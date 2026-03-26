# What Is Clustering? A Deep Dive into Unsupervised Learning and Cluster Partitions

_Chapter 9 of Data Analytics Models and Algorithms — Abstract & Section 9.1_

A few things I made sure to include given you want to actually _learn_ from this:

- A plain-English explanation of all four clustering models (hard, fuzzy, possibilistic, noise) and why each exists
- A breakdown of why each of the three partition conditions matters individually — not just what they say, but what goes wrong if you drop them
- An explanation of why $c$ is bounded at both ends ($c=1$ and $c=n$ are both trivially useless for different reasons)
- A forward-looking "What's Next" section to prime you for what follows

---

## Introduction

Most of what we think of as "machine learning" involves a teacher. You feed a model labelled examples — images tagged as "cat" or "dog", emails marked as "spam" or "not spam" — and the model learns to reproduce those labels for new, unseen inputs. This is **supervised learning**, and it underpins a huge swathe of modern AI.

But what happens when there are no labels? What if you have a vast dataset and no one has told you what anything means? This is the reality in many real-world applications. Medical researchers may have thousands of patient records with no pre-existing diagnoses. A retail company may have years of customer transaction data but no agreed-upon definition of what a "type" of customer even is. An astronomer may have spectra from millions of stars that have never been systematically categorised.

This is where **clustering** comes in — one of the most fundamental and widely used techniques in the field of **unsupervised learning**.

---

## The Core Idea: Learning Without Labels

Clustering is the process of identifying structure in **unlabelled data**. Rather than being told "these points belong to class A and those to class B", a clustering algorithm examines the data itself — its geometry, density, distances, or relationships — and autonomously decides how to group the points into meaningful subsets called **clusters**.

This is a profound shift in perspective. Instead of asking "which pre-defined category does this belong to?", clustering asks "what natural groupings exist in this data at all?"

### When Labels Exist — But Are Ignored

An important and subtle point: clustering can be applied to data that _does_ have class labels. The classic example is the **Iris dataset**, which contains measurements of flower petals and sepals from three labelled species. A clustering algorithm doesn't see those species labels — it only sees the numbers.

The resulting clusters may or may not align with the true botanical species. Sometimes they do, confirming that the classes are geometrically well-separated. Sometimes they don't, suggesting that the class boundaries are more complex than simple geometric proximity. Either way, the clusters are valid structures in their own right — they just describe the data differently from the human-assigned labels.

This is a crucial conceptual point: **clusters are not the same as classes**. Clusters are discovered; classes are defined. Clusters often _serve as_ class estimates when no labels are available, but they carry a different epistemological status.

---

## A Taxonomy of Clustering Methods

Chapter 9 surveys a rich landscape of clustering approaches. Before diving into the mathematical details, it helps to have a map.

### Sequential vs. Prototype-Based Clustering

At the highest level, clustering methods split into two major families:

**Sequential clustering** (also called hierarchical clustering) builds up a cluster structure step by step by successively merging or splitting groups. Methods in this family include:

- **Single linkage** — merges clusters based on the closest pair of points between them
- **Complete linkage** — merges based on the furthest pair
- **Average linkage** — merges based on the average distance between all inter-cluster point pairs
- **Ward's method** — merges clusters to minimise the increase in total within-cluster variance

These methods produce a **hierarchical structure** — a nested tree of clusters called a **dendrogram** — which is extremely informative and doesn't require you to specify the number of clusters in advance. The trade-off is computational cost: sequential methods are expensive, and this limits their applicability to very large datasets.

**Prototype-based clustering** takes a different approach. It represents each cluster by a **prototype** — a summary object that characterises the cluster — and assigns data points to clusters based on their relationship to these prototypes. The famous **k-means** algorithm is the canonical example, where each cluster is represented by its centroid (mean point). Prototype-based methods are generally much more scalable than sequential ones.

### Clustering Models: How "Hard" Is Membership?

Within prototype-based clustering, there is another important dimension: how definitively do we assign a point to a cluster?

- **Hard clustering** — each point belongs to exactly one cluster, with no ambiguity. k-means is a hard clustering algorithm.
- **Fuzzy clustering** — each point has a _degree of membership_ in every cluster, expressed as a number between 0 and 1. A point on the boundary between two clusters might have memberships of 0.6 and 0.4, rather than being forced into one or the other.
- **Possibilistic clustering** — similar to fuzzy, but membership values represent _typicality_ (how well a point fits a cluster) rather than strict partitioning. Memberships no longer need to sum to 1 across clusters.
- **Noise clustering** — explicitly models the possibility that some data points don't belong to any cluster at all. This is essential for robust real-world applications where outliers and irrelevant data points are common.

### Prototype Shapes

The shape of a prototype determines what kind of cluster structure the algorithm can detect:

- **Hyperspheric** prototypes (like k-means centroids) find round, blob-shaped clusters
- **Ellipsoidal** prototypes can detect elongated or rotated clusters
- **Linear** prototypes represent clusters that follow a line or plane
- **Complex shapes** allow for curved or otherwise irregular cluster boundaries

This matters enormously in practice. If your data forms two elongated ellipses at an angle to each other, a hyperspheric prototype method will do a poor job — it will try to force the data into round clusters.

### Other Characteristics

Clustering methods also vary in how they handle the data itself:

- **Medoid-based** methods use actual data points as prototypes, rather than computed averages. This is useful when the "average" of a set of objects isn't meaningful — for example, clustering DNA sequences or graphs.
- **Relational clustering** works directly with a **dissimilarity matrix** (pairwise distances or similarities between objects) rather than raw feature vectors. This is powerful when the objects are complex and hard to represent numerically.
- **Kernelized clustering** applies the kernel trick — projecting data into a higher-dimensional feature space — to find clusters that are non-linearly separable in the original space.
- **Heuristic methods**, such as **self-organizing maps (SOMs)**, use biologically-inspired learning rules to organise data onto a low-dimensional grid.

### Assessing and Validating Clusters

Before running any clustering algorithm, it's worth asking: _does the data actually have a cluster structure?_ If the data is uniformly distributed, any clustering algorithm will produce outputs, but they won't be meaningful. **Cluster tendency assessment** addresses this question.

Once clusters are found, **cluster validity measures** help answer a different question: _how many clusters are there, really?_ Since most algorithms require you to specify the number of clusters $c$ in advance, validity measures provide a data-driven way to evaluate different values of $c$ and choose the best one.

---

## Section 9.1 — Cluster Partitions: The Mathematics of Grouping

With the conceptual landscape in place, let's get precise. Section 9.1 lays down the formal mathematical foundation for what it even means to partition a dataset into clusters.

### Setting the Scene: An Illustrative Example

Consider the following small dataset of six two-dimensional points:

$$X = {(2,2),\ (3,2),\ (4,3),\ (6,7),\ (7,8),\ (8,8)}$$

If you were to plot these on a scatter graph, you'd immediately notice that the points fall into two natural groups: one cluster in the bottom-left corner (the first three points) and one in the top-right corner (the last three). This intuition is the starting point for everything that follows.

The cluster structure partitions $X$ into two **disjoint subsets**:

$$C_1 = {x_1, x_2, x_3} = {(2,2), (3,2), (4,3)}$$ $$C_2 = {x_4, x_5, x_6} = {(6,7), (7,8), (8,8)}$$

This example seems almost trivially obvious — but formalising it carefully is essential, because when you move to high-dimensional data with thousands of points, your geometric intuition no longer works and you need the mathematics to carry the load.

### The Formal Definition of a Cluster Partition

More generally, clustering takes a dataset $X = {x_1, \dots, x_n} \subset \mathbb{R}^p$ — that is, $n$ data points each with $p$ features — and partitions it into $c$ clusters, where $c$ can be any integer from 2 to $n-1$. The partition ${C_1, \dots, C_c}$ must satisfy three conditions:

**Condition 1 — Coverage (Union equals the whole dataset):** $$X = C_1 \cup C_2 \cup \cdots \cup C_c$$ Every data point must belong to at least one cluster. No point can be left out.

**Condition 2 — Non-emptiness:** $$C_i \neq \emptyset \quad \text{for all } i = 1, \dots, c$$ Every cluster must contain at least one data point. You can't have a cluster that's empty — that would just be a smaller partition with $c-1$ clusters.

**Condition 3 — Disjointness (No overlap):** $$C_i \cap C_j = \emptyset \quad \text{for all } i \neq j$$ Each data point belongs to exactly one cluster. No point can be shared between clusters.

These three conditions together define what mathematicians call a **partition** of the set $X$. In the context of hard clustering, this is the foundational structure.

### Why These Conditions Matter

Each condition rules out a specific type of degeneracy:

- Without **coverage**, you could simply ignore most of the data and call a small interesting subset a "cluster" — trivially satisfied but useless.
- Without **non-emptiness**, an algorithm could game a quality metric by creating phantom clusters with no members.
- Without **disjointness**, you'd have ambiguity about which cluster a point truly belongs to — a problem that hard clustering is specifically designed to avoid (fuzzy and possibilistic models later relax exactly this condition).

Together, these conditions ensure that the partition is **complete** (covers all the data), **non-trivial** (every cluster is populated), and **unambiguous** (every point has exactly one home).

### The Constraint on the Number of Clusters

Notice that $c$ is constrained to the range ${2, 3, \dots, n-1}$. Why?

- The lower bound of $c = 2$ exists because a "partition" into a single cluster ($c = 1$) is trivial — it just says "everything is one group", which reveals no structure at all.
- The upper bound of $c = n-1$ is less obvious but equally important. If you allowed $c = n$, you'd end up with $n$ singleton clusters — each data point in its own cluster. Again, this is trivial and tells you nothing about the structure of the data. In fact, it's the opposite failure mode: maximum specificity with zero generalisation.

Meaningful clustering happens somewhere in between. Finding that sweet spot — the "right" value of $c$ — is one of the central challenges of the field, and it's exactly what cluster validity measures are designed to address.

---

## The Bigger Picture: Why This Foundation Matters

The partition definition in Section 9.1 might seem abstract, but it has direct practical consequences for every algorithm discussed in Chapter 9.

When k-means converges, what it's actually converging to is a partition satisfying these three conditions — it's looking for the partition that minimises the total within-cluster variance. When hierarchical clustering cuts a dendrogram at a given height, it produces a partition. When fuzzy c-means outputs a membership matrix, that matrix is a _generalisation_ of this partition — relaxing the hard disjointness condition but otherwise preserving the spirit of coverage and non-emptiness.

Understanding partitions formally also helps you reason about edge cases. What happens when two clusters merge in hierarchical clustering? The disjointness condition is maintained throughout. What happens when a fuzzy algorithm assigns a point membership of exactly 1 to one cluster and 0 to all others? It collapses back to a hard partition. The mathematics gives you a precise language to describe these relationships.

---

## Summary

|Concept|Key Idea|
|---|---|
|**Clustering**|Unsupervised learning that finds structure in unlabelled data|
|**Clusters vs. Classes**|Clusters are discovered from data; classes are externally defined|
|**Sequential clustering**|Hierarchical; builds dendrogram; computationally expensive|
|**Prototype-based clustering**|Represents clusters by prototypes; scalable|
|**Hard / Fuzzy / Possibilistic / Noise**|Increasingly flexible models of cluster membership|
|**Prototype shapes**|Determine which cluster geometries can be detected|
|**Cluster partition**|A complete, non-empty, disjoint decomposition of the dataset|
|**Constraint on $c$**|$2 \leq c \leq n-1$; avoids trivial single-cluster or all-singletons cases|

---

## What's Next

With the concept of a cluster partition firmly defined, Chapter 9 proceeds to ask: how do we _represent_ these partitions efficiently? The next section introduces **partition matrices** and **cluster prototypes** — the algebraic machinery that turns the set-theoretic definition above into something an algorithm can actually optimise.

---

_Source: Runkler, T. A. — Data Analytics: Models and Algorithms (Springer, 2025), Chapter 9._
