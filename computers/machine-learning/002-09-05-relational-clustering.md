# Relational Clustering: Finding Clusters Without Feature Vectors

_Chapter 9 of Data Analytics Models and Algorithms — Section 9.5_

The section covers a lot of ground so I structured it around the two main strategies (medoids vs. reformulation) before tackling the two complications (non-Euclidean distances and kernelization).

A few things worth paying particular attention to:

The **equivalence result** between RFCM and FCM when DD D is Euclidean is subtle but important — it tells you the reformulation isn't losing anything, it's genuinely the same algorithm expressed differently. This is a good thing to be able to articulate if asked.

The **kernel trick's soft-clipping effect** is a nice result that ties back to the outlier discussion in Section 9.4. The Gaussian and hyperbolic tangent transformations aren't just enabling complex geometries — they're also passively capping outlier influence as a side effect of their saturation behaviour.

The closing summary captures the most important conceptual point: all these adaptations transform the _data_, not the _algorithm_. The AO loop stays the same throughout. That's a clean mental model to carry into exam questions or applied work.

---

## The Problem: Clustering Without Coordinates

Every clustering method in Sections 9.3 and 9.4 — CM, FCM, PCM, NC — assumes your data lives in a feature space $X \subset \mathbb{R}^p$. Each data point is a coordinate vector, and distances are computed geometrically.

But many real-world datasets don't come as coordinate vectors. You might have:

- A matrix of pairwise edit distances between DNA sequences
- Survey data where respondents rated similarity between products
- A graph of social connections where "distance" is path length
- Perceptual similarity scores from human experiments

What you have is a **distance matrix** $D$ — an $n \times n$ symmetric matrix where $d_{ij}$ is the dissimilarity between objects $i$ and $j$, with $d_{ii} = 0$ and $d_{ij} = d_{ji}$. There are no coordinates. There is no $\mathbb{R}^p$.

This is **relational data**, and clustering it requires either adapting the existing algorithms or transforming the data. Section 9.5 covers both strategies.

---

## What Already Works: Linkage Methods

The good news is that the sequential clustering methods from Section 9.2 — **single linkage, complete linkage, and average linkage** — require only pairwise distances. They never compute cluster centres or reference feature vectors. They work on $D$ directly, out of the box.

The bad news is that the more powerful prototype-based methods (CM, FCM, PCM, NC) require coordinates to compute cluster centres $v_i$ as means of assigned points. Two strategies bridge this gap.

---

## Strategy 1: Medoid-Based Clustering

The core obstacle is that cluster centres $v_i$ are computed as means of data points — a meaningful operation in $\mathbb{R}^p$ but undefined when you only have distances.

The simplest fix: **constrain prototypes to be actual data points**. Instead of a computed mean, each cluster centre must be one of the $n$ objects in the dataset. These constrained prototypes are called **medoids**, and the constraint is simply $V \subseteq X$.

Why does this help? Because $D$ already contains every pairwise distance $d_{jk}$ between data objects. If $v_i = x_j$ (i.e., object $j$ is the medoid of cluster $i$), then the distance $|x_k - v_i|^2 = d_{jk}^2$ is directly available from $D$. No coordinates needed.

This yields a family of relational medoid models:

|Original Model|Medoid Variant|
|---|---|
|C-Means (CM)|Relational C-Medoids (RCMdd)|
|FCM|Relational Fuzzy C-Medoids (RFCMdd)|
|PCM|Relational Possibilistic C-Medoids (RPCMdd)|
|NC|Relational Noise Clustering with Medoids (RNCMdd)|

### How Medoid Selection Works (RFCMdd Example)

The membership matrix $U$ is updated exactly as in FCM — the only change is that distances come from $D$ rather than computed geometry. The challenge is selecting which data points to use as medoids.

The contribution of cluster $i$ to the objective function, assuming medoid $v_i = x_j$, is:

$$J_{ij} = \sum_{k=1}^n u_{ik}^m, d_{jk}^2$$

The best medoid for cluster $i$ is whichever data point minimises this — an **exhaustive search** over all $n$ candidates:

$$w_i = \underset{j \in {1,\dots,n}}{\arg\min}\ J_{ij}$$

This is repeated for each cluster at each AO iteration. The computational cost is significant — $O(n^2)$ distance lookups per cluster per iteration — and grows quickly with $n$. Medoid-based clustering is practical for moderate-sized datasets but not for very large ones.

---

## Strategy 2: Reformulation

A more elegant approach avoids medoid constraints entirely by **algebraically eliminating the cluster centres** from the objective function before solving.

The key insight: the optimal centre formula $v_i = \frac{\sum_k u_{ik}^m x_k}{\sum_k u_{ik}^m}$ (equation 9.28) can be substituted directly into the objective function. After this substitution, $V$ disappears — the objective is expressed purely in terms of $U$ and the pairwise distances $D$.

### The RFCM Objective

For FCM with Euclidean distances, this reformulation yields:

$$J_{RFCM}(U; D) = \sum_{i=1}^c \frac{\displaystyle\sum_{j=1}^n \sum_{k=1}^n u_{ij}^m, u_{ik}^m, d_{jk}^2}{\displaystyle\sum_{j=1}^n u_{ij}^m}$$

This is a function of $U$ and $D$ only — no feature vectors, no explicit centres. The membership update equation becomes correspondingly more complex (equation 9.47 in the text), but the AO structure is identical: iterate on $U$ until convergence.

The full family of reformulated models:

|Original|Reformulated Relational|
|---|---|
|CM|RCM|
|FCM|RFCM|
|PCM|RPCM|
|NC|RNC|

### Equivalence with Feature-Based Methods

A crucial property: **if $D$ was computed from feature data $X$ using the Euclidean norm**, then minimising RFCM over $D$ yields exactly the same partition as minimising FCM over $X$. The reformulation is lossless in the Euclidean case.

This equivalence holds for all the paired models: CM/RCM, FCM/RFCM, PCM/RPCM, NC/RNC, and their medoid variants. It confirms that the reformulation is not an approximation — it's mathematically equivalent to the original when the distances are Euclidean.

---

## The Non-Euclidean Problem

Things break down when $D$ is **not** a Euclidean distance matrix. This happens when:

- Distances are computed using a non-Euclidean norm (e.g. Manhattan, cosine)
- Distances come from domain-specific measurements with no underlying coordinate space

In these cases, the reformulated objective may produce memberships $u_{ik} < 0$ or $u_{ik} > 1$ — outside the valid $[0,1]$ range. The maths is no longer guaranteed to behave.

### The Beta Spread Transformation

The fix is to pre-process $D$ into an approximating Euclidean matrix. The **beta spread transformation** adds a uniform offset $\beta \geq 0$ to all off-diagonal elements:

$$D_\beta = D + \beta \cdot \begin{pmatrix} 0 & 1 & \cdots & 1 \ 1 & 0 & \cdots & 1 \ \vdots & & \ddots & \vdots \ 1 & 1 & \cdots & 0 \end{pmatrix}$$

In practice, start with $\beta = 0$ and increase it incrementally until all memberships stay within $[0, 1]$. The models using this transformation are prefixed with **NE** (Non-Euclidean): **NERFCM**, **NERPCM**, etc.

The beta spread transformation "inflates" all inter-object distances by the same amount, which tends to push the distance matrix toward being Euclidean-embeddable. It's a pragmatic patch rather than a deep geometric solution, but it works reliably in practice.

---

## Kernelization: Handling Complex Geometries

All the relational models above inherit the hyperspherical cluster assumption from their CM/FCM/PCM/NC parents. For non-spherical cluster shapes in feature data, Section 9.4 addressed this by changing the distance function (Gustafson-Kessel, FCV, FCS, etc.). In relational data, there are no coordinates to apply those geometric transformations to.

The solution: **the kernel trick** — the same technique used in Support Vector Machines (Chapter 8) to find nonlinear decision boundaries.

### The Kernel Trick for Distances

The kernel trick implicitly maps data into a high-dimensional feature space $\phi: \mathbb{R}^p \to \mathcal{H}$ without ever computing $\phi(x)$ explicitly. Instead, all computations are expressed through **kernel evaluations** $k(x_j, x_k) = \phi(x_j) \cdot \phi(x_k)^T$.

For relational clustering, the key result is that the squared Euclidean distance in the kernel space can be written entirely in terms of kernel evaluations:

$$d_{jk}^{\prime 2} = |\phi(x_j) - \phi(x_k)|^2 = k(x_j, x_j) - 2k(x_j, x_k) + k(x_k, x_k)$$

Assuming normalised kernels where $k(x, x) = 1$ for all $x$, this simplifies to:

$$d_{jk}^{\prime 2} = 2 - 2 \cdot k(x_j, x_k)$$

This means **kernelizing a relational clustering algorithm is just a preprocessing step**: replace the distance matrix $D$ with a kernelized matrix $D'$ computed by the formula above, then run the unmodified clustering algorithm on $D'$.

### The Two Standard Kernel Transformations

For the **Gaussian kernel** $k(x_j, x_k) = e^{-d_{jk}^2/\sigma^2}$:

$$d_{jk}^{\prime 2} = 2 - 2e^{-d_{jk}^2/\sigma^2}$$

For the **hyperbolic tangent kernel** $k(x_j, x_k) = \tanh(d_{jk}^2/\sigma^2)$:

$$d_{jk}^{\prime 2} = 2\tanh!\left(\frac{d_{jk}^2}{\sigma^2}\right)$$

Both transformations share an important geometric property: **small distances are scaled approximately linearly**, but **large distances are soft-clipped** at a threshold near $\sqrt{2}$. The parameter $\sigma$ controls where the clipping kicks in.

Because all relational clustering algorithms are invariant to uniform scaling of $D$, the absolute values of the transformed distances don't matter — only their relative magnitudes. This means you can think of the kernel transformation purely in terms of its **shape**: linear for small $d$, saturating for large $d$.

### Why Kernelization Helps with Outliers

The soft-clipping behaviour has a direct practical benefit: **outliers are defanged**. An outlier at distance $d_{jk} \gg \sigma$ from everything else would dominate the objective function in plain relational clustering — its large squared distance contributes enormously to $J$. After kernel transformation, that same distance is clipped to approximately $\sqrt{2}$, capping its influence.

This makes kernelized relational clustering inherently more robust to outliers than its non-kernelized counterpart — a bonus on top of the ability to handle non-spherical cluster geometries.

The kernelized model family is denoted with a **k** prefix: **kCM**, **kFCM**, **kPCM**, **kNERFCM**, **kNERPCM**, and so on.

---

## The Full Landscape

Here is the complete relational clustering model family from Section 9.5:

|Scenario|Model Family|
|---|---|
|Euclidean distances, medoid prototypes|RCMdd, RFCMdd, RPCMdd, RNCMdd|
|Euclidean distances, reformulated|RCM, RFCM, RPCM, RNC|
|Non-Euclidean distances, beta spread|NERFCM, NERPCM, …|
|Kernelized (any distance)|kCM, kFCM, kPCM, kNERFCM, kNERPCM, …|

The linkage methods (single, complete, average) work on any distance matrix without modification and sit outside this hierarchy entirely.

---

## Summary

| Concept                   | Key Point                                                                                |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| **Relational data**       | Only pairwise distances $D$ available; no feature vectors                                |
| **Linkage methods**       | Already work on $D$ natively                                                             |
| **Medoid constraint**     | Restrict prototypes to actual data points; use $D$ for all distances                     |
| **Reformulation**         | Eliminate centres algebraically; objective becomes a function of $U$ and $D$ only        |
| **Euclidean equivalence** | RFCM = FCM when $D$ is Euclidean; reformulation is lossless                              |
| **Non-Euclidean $D$**     | May yield invalid memberships; fix with beta spread transformation (NE prefix)           |
| **Kernel trick**          | Replace $D$ with $D' = 2 - 2k(x_j, x_k)$; enables complex cluster geometries             |
| **Soft-clipping effect**  | Kernel transformation caps the influence of large distances, suppressing outlier effects |

The central lesson of Section 9.5: **the structure of the clustering models is preserved across all these adaptations**. Whether you use medoids, reformulation, beta spread, or kernelization, the AO loop and the membership/prototype update equations remain recognisably the same. The transformations happen to the _data_, not to the _algorithm_.

---

_Source: Runkler, T. A. — Data Analytics: Models and Algorithms (Springer, 2025), Chapter 9._
