# Hierarchical Clustering and the C-Means Model

_Chapter 9 of Data Analytics Models and Algorithms — Sections 9.2 & 9.3_

A few things worth flagging as you read:

- The **chaining problem** in single linkage is something exam questions love — it's the main reason you'd choose complete or Ward's over single linkage in practice
- The **partition matrix** in 9.3 is worth paying close attention to — it's a small idea that does a lot of work in the chapters that follow (fuzzy clustering is literally just relaxing one constraint on it)
- The **alternating optimisation** loop is essentially the entirety of k-means, just named more formally — recognising it as AO helps when you later see other models that use the same pattern

---

## Section 9.2 — Sequential Clustering

### The Core Idea: Build a Hierarchy Bottom-Up

The most important family of sequential clustering methods is **SAHN** — Sequential Agglomerative Hierarchical Nonoverlapping clustering. The algorithm is conceptually simple:

1. Start by treating every single data point as its own cluster. With $n$ points, you begin with $n$ clusters: $\Gamma_n = {{o_1}, \dots, {o_n}}$
2. At each step, find the two clusters that are _least dissimilar_ and merge them into one
3. Repeat until you reach the desired number of clusters, or until everything has been merged into a single cluster: $\Gamma_1 = {{o_1, \dots, o_n}}$

Each merge reduces the cluster count by one, so after $n - c$ merges you have $c$ clusters. The result is not just a single partition but a **nested hierarchy** of partitions — every partition at level $c$ is a refinement of the partition at level $c-1$.

### The Five Linkage Measures

The key decision in SAHN is how you measure the dissimilarity between two clusters $C_r$ and $C_s$. Five options are defined, each with different geometric behaviour.

The first three work on any data — including relational data where you only have pairwise distances, not raw feature vectors:

**Single linkage (minimum distance):** $$d(C_r, C_s) = \min_{x \in C_r,\ y \in C_s} d(x, y)$$ The distance between the two _closest_ points across the clusters. Single linkage is the most popular measure, but it has a well-known weakness: it tends to produce long, stringy, chain-like clusters rather than compact blobs. A single bridge point between two otherwise well-separated groups can cause them to merge prematurely.

**Complete linkage (maximum distance):** $$d(C_r, C_s) = \max_{x \in C_r,\ y \in C_s} d(x, y)$$ The distance between the two _furthest_ points. This produces tighter, more compact clusters, because two clusters only merge when every point in one is reasonably close to every point in the other.

**Average linkage:** $$d(C_r, C_s) = \frac{1}{|C_r| \cdot |C_s|} \sum_{x \in C_r,\ y \in C_s} d(x, y)$$ The average of _all_ pairwise distances between the two clusters. A pragmatic middle ground between the extremes of single and complete linkage.

The next two are defined only for **feature data** (where actual coordinate vectors exist):

**Distance of centres:** $$d(C_r, C_s) = \left| \frac{1}{|C_r|} \sum_{x \in C_r} x - \frac{1}{|C_s|} \sum_{x \in C_s} x \right|$$ Simply the Euclidean distance between the two cluster centroids. Intuitive, but it can be fooled when clusters have very different sizes or densities.

**Ward's measure:** $$d(C_r, C_s) = \frac{|C_r| \cdot |C_s|}{|C_r| + |C_s|} \left| \frac{1}{|C_r|} \sum_{x \in C_r} x - \frac{1}{|C_s|} \sum_{x \in C_s} x \right|$$ Ward's method merges the pair of clusters that causes the _smallest increase in total within-cluster variance_. The formula is a weighted centroid distance — the weighting accounts for cluster sizes so that merging two large clusters is penalised more heavily than merging two small ones. In practice, Ward's method often produces the most visually natural, balanced clusters.

> **Rule of thumb:** single linkage finds chains, complete linkage finds blobs, Ward's method finds balanced compact groups. The right choice depends on the geometry you expect in your data.

### Dendrograms

The hierarchical output of SAHN is typically visualised as a **dendrogram** — a tree diagram where:

- The horizontal axis lists the individual data points
- The vertical axis represents the dissimilarity at which each merge occurred
- Each horizontal bar connecting two branches shows the level at which those clusters were joined

For the six-point example dataset $X = {(2,2),(3,2),(4,3),(6,7),(7,8),(8,8)}$ using single linkage, the full sequence of partitions is:

| Level                 | Partition                                                               |
| --------------------- | ----------------------------------------------------------------------- |
| $\Gamma_6$            | ${{x_1}, {x_2}, {x_3}, {x_4}, {x_5}, {x_6}}$ — all singletons           |
| $\Gamma_5 = \Gamma_4$ | ${{x_1, x_2}, {x_3}, {x_4}, {x_5, x_6}}$ — closest pairs merge first    |
| $\Gamma_3 = \Gamma_2$ | ${{x_1, x_2, x_3}, {x_4, x_5, x_6}}$ — the natural two-cluster solution |
| $\Gamma_1$            | ${X}$ — everything merged                                               |

Notice $\Gamma_5 = \Gamma_4$ and $\Gamma_3 = \Gamma_2$. This happens when two merges occur at the same (or very similar) distance — the partition doesn't change between those levels.

The dendrogram encodes the entire merge history. To extract any particular $c$-partition, you simply "cut" the dendrogram horizontally at the appropriate height.

### Variants and Complexity

**DBSCAN** is a notable variant that replaces distance-based linkage with density estimation. Rather than always merging the closest clusters, DBSCAN defines clusters as dense regions separated by sparse regions, and explicitly labels low-density points as _noise_. This makes it robust to outliers and capable of finding clusters of arbitrary shape — something standard SAHN linkages struggle with.

**SDHN** (Sequential Divisive Hierarchical Nonoverlapping) is the reverse: start with all points in one cluster and successively split. This top-down approach is conceptually symmetric, but splitting a cluster is a much harder problem than merging two (there are exponentially many ways to split), so SDHN is far less common in practice.

**Computational cost** is the main limitation of SAHN. The naive algorithm runs in $O(n^3)$ time. More efficient implementations bring this down to $O(n^2 \log n)$ for general SAHN and $O(n^2)$ for single linkage specifically — but even $O(n^2)$ becomes prohibitive for datasets with millions of points. This is why sequential clustering is typically reserved for smaller datasets or used as a post-processing step on already-compressed representations.

---

## Section 9.3 — Prototype-Based Clustering

### A New Way to Represent Clusters: The Partition Matrix

Section 9.1 represented a cluster partition as a collection of sets. Section 9.3 introduces an equivalent but algebraically more useful representation: the **partition matrix** $U$.

$U$ is a $c \times n$ matrix where each entry $u_{ik}$ is defined as:

$$u_{ik} = \begin{cases} 1 & \text{if } x_k \in C_i \ 0 & \text{if } x_k \notin C_i \end{cases}$$

In other words, row $i$ is a binary vector that "lights up" exactly the points belonging to cluster $i$. Two constraints enforce the partition properties:

- **Non-empty clusters:** $\sum_{k=1}^n u_{ik} > 0$ for all $i$ — every row has at least one 1
- **Hard partition:** $\sum_{i=1}^c u_{ik} = 1$ for all $k$ — every column sums to exactly 1 (each point belongs to exactly one cluster)

This matrix formulation is powerful because it opens the door to generalisation. Relax the second constraint — allow $u_{ik} \in [0, 1]$ instead of ${0, 1}$ — and you immediately have **fuzzy clustering**. The partition matrix is the algebraic hinge on which all later clustering models pivot.

### Cluster Prototypes: Representing Clusters by Their Centres

Beyond sets and matrices, a third way to represent a cluster structure is through **prototypes**. The simplest prototype is a **centre** (centroid) — a single point $v_i \in \mathbb{R}^p$ that summarises cluster $C_i$. The full cluster structure is then described by the set:

$$V = {v_1, \dots, v_c} \subset \mathbb{R}^p$$

This is appealingly compact: instead of storing which of the $n$ points belongs to each cluster, you just store $c$ representative points.

### The C-Means Objective Function

Given a dataset $X$, how do you find good centres $V$ and a good partition $U$? The **c-means (CM) model** formalises "good" as minimising the total squared distance from each point to its assigned cluster centre:

$$J_{CM}(U, V; X) = \sum_{i=1}^c \sum_{x_k \in C_i} |x_k - v_i|^2 = \sum_{i=1}^c \sum_{k=1}^n u_{ik} |x_k - v_i|^2$$

The two forms are equivalent — the partition matrix $u_{ik}$ simply zeroes out the distance terms for points not in cluster $i$. Minimising $J_{CM}$ is the goal; the question is how.

### The Two Optimality Conditions

Minimising $J_{CM}$ yields closed-form solutions for both $U$ and $V$, but with a catch: each optimal solution depends on the other.

**Optimal $U$ given $V$:** Assign each point to its nearest centre. For each data point $x_k$:

$$u_{ik} = \begin{cases} 1 & \text{if } |x_k - v_i| = \min_{j=1,\dots,c} |x_k - v_j| \ 0 & \text{otherwise} \end{cases}$$

This is just the **nearest-neighbour rule** — put each point in the cluster whose centre is closest to it.

**Optimal $V$ given $U$:** Take the derivative of $J_{CM}$ with respect to $v_i$, set it to zero, and solve:

$$v_i = \frac{\sum_{k=1}^n u_{ik} x_k}{\sum_{k=1}^n u_{ik}} = \frac{1}{|C_i|} \sum_{x_k \in C_i} x_k$$

Each cluster centre is simply the **mean** of the points currently assigned to it. This is where the name "c-means" (and its more common alias, **k-means**) comes from.

### Alternating Optimisation

Since the optimal $U$ depends on $V$ and the optimal $V$ depends on $U$, neither can be solved in isolation. The solution is **alternating optimisation (AO)**:

1. Initialise $V$ (e.g. randomly, or by picking $c$ data points at random)
2. Compute $U$ from $V$ using the nearest-neighbour rule
3. Compute $V$ from $U$ by taking cluster means
4. Repeat steps 2–3 until $V$ stops changing (convergence)

This is guaranteed to converge because each step can only decrease or maintain $J_{CM}$ — it never increases it. However, it is only guaranteed to find a **local minimum**, not a global one. Different initialisations can yield different final partitions, which is why k-means is often run multiple times with different random seeds.

A **reverse AO** variant initialises $U$ instead and terminates on $U$. When $p < n$ (more data points than features, the common case), the standard AO variant is more efficient because $V$ is $c \times p$ and $U$ is $c \times n$, and updating the smaller matrix first reduces computation.

### Ties

One subtlety: when a point $x_k$ is exactly equidistant from two or more centres, the argmin in the partition update is not unique. This must be handled explicitly — a common approach is random assignment, though other heuristics exist. Ties rarely cause problems in practice but are worth being aware of when implementing or debugging.

---

## Summary

|Concept|Key Point|
|---|---|
|**SAHN**|Agglomerative; starts with $n$ singletons, merges up to desired $c$|
|**Linkage measures**|Single (min), complete (max), average, centre distance, Ward's|
|**Single linkage**|Popular but prone to chaining; others produce more compact clusters|
|**Dendrogram**|Tree diagram encoding the full merge hierarchy; cut at any height to get a $c$-partition|
|**DBSCAN**|Density-based SAHN variant; handles noise and arbitrary shapes|
|**SDHN**|Divisive (top-down) variant; less common due to difficulty of splitting|
|**SAHN complexity**|$O(n^3)$ naive; $O(n^2 \log n)$ improved; $O(n^2)$ for single linkage|
|**Partition matrix $U$**|Binary $c \times n$ matrix encoding cluster membership; generalises to fuzzy models|
|**C-means objective $J_{CM}$**|Total squared distance from points to their assigned centres|
|**Optimal $U$**|Nearest-neighbour assignment|
|**Optimal $V$**|Cluster means|
|**Alternating optimisation**|Iteratively update $U$ and $V$; converges to a local minimum|

---

_Source: Runkler, T. A. — Data Analytics: Models and Algorithms (Springer, 2025), Chapter 9._
