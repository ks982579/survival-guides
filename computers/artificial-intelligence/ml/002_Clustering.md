# Machine Learning

```yaml
title: Machine Learning
code: DLMDSML01
authors: n/a
date: 2024-04-10
publisher: IU Internationale Hochschule Gmbh
publisher_en: IU International University of Applied Sciences
version: 001-2024-0410
```

# 2. Clustering

pp. 31-66

The goal is to learn:
- What is meant by *clustering*.
- Common applications of clustering analysis.
- The different methods for clustering analysis.
- The implementation of clustering methods in Python.
- The advantages and limitations of each clustering method.

## Introduction

**Unsupervised Learning** denotes the machine learning task of pattern or structure discovery in unlabeled datasets. It addresses use cases where no labels or desired outcomes are given. We can either:
- cluster data to reveal meaningful partitions and/or hierarchies;
- cluster data to find association rules that interrelate the involved data's variables
	- e.g. how frequently two products are bought together.

**Clustering** means to gather data records into natural groups (i.e. clusters) of similar samples according to predefined similarity/dissimilarity metrics. This results in extracting a set of useful information about the given dataset. 
- Contents of any cluster should be similar to each other. 
	- called "high intra-cluster similarity".
- Contents of any cluster should be very dissimilar from the contents of other clusters
	- called "high inter-cluster separation".

The similarity/dissimilarity metric routinely utilized in clustering analysis is a form of distance function between each pair of records. 

Two common and simple forms of distance function:

**Euclidean distance**

$$
\begin{align}
d_{A,B} &= \sqrt{(x_A-x_B)^2 + (y_A-y_B)^2}
\end{align}
$$

**Manhattan Distance**:

$$
\begin{align}
d_{A,B} &= |x_A-x_B| + |y_A-y_B |
\end{align}
$$

Where $(x_A, y_A)$ and $(x_B, y_B)$ are the coordinates, or **features**, of the data records A and B respectively. A **Feature** is a measurable and observable quantity about the data record. Value $d$ represents the distance between the two data records. 

Note: features of the datasets that have scales with widely differing ranges should be *standardized* to the same scale before progressing in any form of clustering analysis.

To complete clustering evaluation:
- manual inspection of results
- benchmarking on existing labels
- distance measures to denote the similarity level within a cluster and the dissimilarity level across the clusters. 

**Clustering Analysis** is a type of unsupervised learning that sorts a set of data records into clusters or groups. Clustering analysis is applied in many fields including:
- Pattern recognition
- image processing
- spatial data analysis
- bioinformatics
- crime analysis
- medical imaging
- climatology
- robotics

A noteworthy area of clustering applications is *market segmentation*, which focuses on grouping customers into cluster of different characteristics:
- payment history
- customers' interests
- etc...

This information is then used for targeted marketing.

Another common application is to implement clustering analysis to develop a *recommendation system*. An example here is to cluster similar documents together or to recommend similar songs/movies!

Clustering analysis is an active area of research. Some main classes of methods and techniques, based on broad approaches of how grouping is performed, are:
- Centroid-based clustering methods.
- Gaussian mixtures models clustering methods.
- Hierarchical clustering methods.
- Density based clustering methods.

## 2.1 Centroid-Based Clustering

p. 33

**Centroid-based** clustering searches for a pre-determined number of clusters within an unlabeled and possibly multidimensional dataset. 

A **Centroid** is the arithmetic average position of all the points of data. It may be located at a given point (real centroid) or at a new placement (imaginary centroid).

Each data record is assigned to one, and only one, cluster. That is, there are no intersections between clusters, they do not overlap. 

The rule is that the distance between a data record and each of the cluster's *centroids* is calculated, and this data record is assigned to the cluster achieving the minimum distance.

### 2.1.1 K-Means Clustering

**K-means clustering** is a centroid-based clustering approach commonly used in practice. This method partitions n data records from the given dataset into K clusters. This approach consists of three main steps:
- Initialization
	- Number of clusters are assumed (i.e.; K is predetermined).
	- Centroid of each cluster is randomly defined. 
	- To find initial placement of a cluster's centroid
		- give it the location of one of the given data records. 
		- Prudent to locate the centroids far from each other to span the whole domain of data records. 
- Assignment
	- Clusters are formed by connecting data records with nearest centroid. 
- Update step
	- More accurate centroids of each cluster are calculated as the mean point of its included data records. 
	- Assignment and update steps are repeated until *convergence*
		- when no changes are calculated in clusters' centroids.

The course book shows an example then with 19 data points. 

They calculate the Euclidean distance to each cluster's centroid. Calculate for all centroids and assign to the one that is closest. 

#### K-Means in Python

p. 39

The course book provides an example in python. 

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from pandas import DataFrame
from sklearn.cluster import KMeans

data = {'x': [...], 'y': [...]}
df = DataFrame( Data, columns=['x', 'y'] )
kmeans = KMeans(n_clusters=3).fit(df)

# Find Centroids fo clusters
centroids = kmeans.cluster_centers_

# Associated Cluster for each record
labels: array = kmeans.labels_

# display cluster contents and centroids
plt.scatter(df['x'], df['y'], c=kmeans.labels_.astype(float),
s=50, alpha=0.5)
# That is a cool plot!!!

# Use model to predict 
kmeans.predict([[20, 20], [60, 40]])
# >> array([1,0])
```

Default function of `KMeans()` in Python is written with main parameters as:

```python
KMeans(
	n_clusters=8,
	init='kmeans++',
	n_init=10,
	max_iter=300,
	tol=0.0001,
	precompute_distance='auto'
)
```

What these mean:
- n-cluster = cluster and centroids.
- init = method of initialization
	- k-means++ selects initial centroids in smart way to speed up convergence. 
	- 'random' is obvious
- n-init = number of times k-means algorithm will run with different centroid seeds.
- max-iter = max for a single run
- tol = tolerance regarding declaring convergence
- precompute-distances 
	- 'auto' = do not precompute distances if $sample_n * cluster_n > 12*10^6$. 
		- corresponds to about 100MB overhead per job w/double precision
	- True = always pre-compute distances
	- False = never!

#### Limitations of K-Means

p. 41

K-means clustering techniques is relatively simple to employ. 
- suitably efficient for large datasets
- assumes convergence
- can easily assume initial centroids' placements
- smoothly adjusts the clusters' outlines when new data records are introduced.

However:
- the user must first determine the number of clusters
	- this is significantly difficult to predict. 
- Different initial partitions can result in different final clusters.

Also:
- K-means assumes a *spherical* shape of clusters.
	- not good technique if dataset has regions with differently shaped densities.
- K-means only handles numerical datasets. 
- Initial assumption of centroids may result in poor convergence rate. 
- Normalization of dataset may produce different results.
- Using k-means with standard Euclidian distance measure is not well-suited for high-dimensional data. 

If dataset is dynamic over time:
- extra burden of checking optimum number of clusters periodically.

And fake outliers may not be detected and influence the structures of clusters.

Computational complexity
- $M$ iterations
- $n$ records
- $K$ centroids
- Complexity of $O(M \times n \times K)$

## 2.2 Gaussian Mixture Models Clustering

p. 42

K-means clustering performs a *hard* clustering and generates circular clusters centered at the found centroids.

In **Gaussian Mixture Models** (GMM) clustering, each cluster is considered a **probabilistic generative model**. 
- A **probabilistic generative model** explains how the input data are generated in terms of their joint probability distribution. 

The idea:
- A data record has a probability for belonging to each cluster. 
- It is assigned to those returning highest probability
- This is a *soft* clustering. 

Like the K-means method, GMM also initially assumes the number of clusters for the input dataset. GMM tries to fit mixtures of Gaussian distributions to the dataset, where each distribution defines one cluster.

Each cluster in GMM clustering follows a Gaussian distribution with two parameters
- Cluster's mean: $\mu$
- Standard deviation: $\sigma$

When the inferred GMM clusters have equal and diagonal covariance matrix (i.e. circular shapes), result is equivalent to k-means clustering result.

In general, the task for GMM clustering is:
- Find optimum values for $\mu$ and $\sigma$ to maximize overall probability (or likelihood) of data records to be in their assigned clusters. 
- To achieve = expectation maximization algorithm is implemented.

### 2.2.1 Expectation Maximization Algorithm

p. 43

The **Expectation Maximization** (EM) algorithm is implemented when:
- There is an analytic model for the dataset
	- i.e. the probabilistic Gaussian mixtures model
- The model's shape is known.
	- i.e. Gaussian distribution.
- Parameters $\mu$ and $\sigma$ are not known.

Here, the EM algorithm is an iterative method to find the maximum likelihood estimates of these parameters to get the best fit model and stops when a desired convergence criterion is achieved. 

Gaussian Mixtures Model (GMM) is defined as:
- a set of $K$ probability distributions
	- Each distribution corresponds to one cluster
- A data record is assigned a membership probability for each cluster
- We assign a data record to a cluster based on the largest probability value. 

The algorithm has two steps
- Expectation Step (E)
- Maximization Step (M)

Step 1: Assume the number of clusters $(K)$. Guess initial parameter values for each cluster, $\mu_k$ and $\sigma_k$ for $k = 1, \dots, K$. 

We assume a weight for each cluster, which is the probability that any given data record is a member of that specific cluster, $q_k$. We can start with assuming that $q_k$ is equal for all clusters.

$$
\sum_1^K q_k = 1
$$

Step 2: E Step:

Compute the membership probability for each data record, $(x_i, i = 1, \dots, n)$ in each cluster ($k$):

$$
\begin{align}
P(x_i | k) &= \frac{1}{\sqrt{(2 \pi)^n \sigma_k^2}} \cdot e^{-\frac{(x_i - \mu_k)^T \cdot (x_i - \mu_k)}{2\sigma_k^2}}
\end{align}
$$

Then construct an expression for the likelihood of all data records, which is the responsibilities of each distribution for each data point.

The probability that $x_i$ belongs to cluster $k$ *over* the total probability for $x_i$

$$
r_{ik} = \frac{q_k \cdot P(x_i k)}{\sum_1^K{q_k \cdot P(x_i k)}}
$$

If $x_i$ is very close to one cluster $k$ then the $r_{ik}$ value will be high for it.

Step 3: The M Step:

For each cluster $k$, calculate the total likelihood $m_k$:

$$
\begin{align}
m_k &= \sum_{i=1}^n{r_{ik}} \\
k &= 1, \dots, K
\end{align}
$$

Update initially assumed parameters (recalculate mean and std):

$$
\begin{align}
q_k' &= \frac{m_k}{\sum_1^K{m_k}} \\
\mu_k' &= \frac{1}{m_k} \sum_{i=1}^n{r_ik \cdot x_i} \\
\sigma_k'^2 &= \frac{1}{m_k} \sum_{i=1}{n}{r_ik \cdot (x_i - \mu_k')^T \cdot (x_i - \mu_k')} \\
\end{align}
$$

Then iterate through the two steps until no further changes in the parameters are noted, or when the log-likelihood function (below) converges:

$$
\sum_{i=1}^{N}{\left( \ln{ \left( \sum_{k=1}^{K}{q_k' \cdot P(x_i k)} \right)} \right)}
$$

Finally, Assign each data record to the cluster that it has the highest membership probability. 

These calculations can be quite heavy. Luckily, we can utilize Python to solve GMM clustering problems. The book uses the Iris dataset, well known

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from pandas import DataFrame
from sklearn import datasets
from sklearn.mixture import GaussianMixture

# load the iris dataset
iris = datasets.load_iris()

# select first two columns
X = iris.data[:, :2]

# turn it into a dataframe
d = pd.DataFrame(X)

# plot the data
plt.scatter(d[0], d[1])

# Shows data plotted on graph
plt.show()

# fit the data as a mixture of 3 Gaussians
gmm = GaussianMixture(n_components = 3)
gmm.fit(d)

# predict the cluster of each data record
labels = gmm.predict(d)

# Check if the model has converged
print('Converged:',gmm.converged_)
## Converged: True

# print the number of iterations needed
print(gmm.n_iter_)
## 8

# get the final “means” for each cluster
means = gmm.means_
print(means)
## array([[5.9009976 , 2.74387546],
## [5.01507898, 3.4514463 ],
## [6.68055626, 3.02849627]])

# get the final “standard deviations” (i.e., covariance matrix)
for each cluster
covariances = gmm.covariances_
print(covariances)
## array([[[0.27671149, 0.08897036],
## [0.08897036, 0.09389206]],
## [[0.11944714, 0.08835648],
## [0.08835648, 0.11893388]],
## [[0.36153508, 0.05159664],
## [0.05159664, 0.08927917]]])

# plot the data records in each clusters in different color
d['labels']= labels
d0 = d[d['labels']== 0]
d1 = d[d['labels']== 1]
d2 = d[d['labels']== 2]
plt.scatter(d0[0], d0[1], c ='r')
plt.scatter(d1[0], d1[1], c ='yellow')
plt.scatter(d2[0], d2[1], c ='g')

plt.show()
```

### 2.2.2 Limitation of GMM Clustering

p. 47

We prefer GMM clustering for datasets consisting of regions that do not look like simple circles. However, they should still be in shapes, maybe just more complex ones, such as ellipsoids. 

It is also the method of choice if it is desirable to know the probability of a data record to belong to each of the clusters. 

This technique can simultaneously optimize a large number of variables to create both "hard" clusters with crisp 0-1 membership encoding, and the "soft" clusters with soft borders according to the probability level (i.e. membership) of each data record. 

But be warned, with big and complex maths, the EM algorithm can be slow because it is time consuming to find the probability distribution for each data record. It may also get *stuck* in a local maximum of the log-likelihood function (instead of the global).

The steps, in general, suffer from heavy computations of the conditional probabilities. 

## 2.3 Hierarchical Clustering 

p. 47

Hierarchical clustering solves the challenge of needing to know (or decide) the number of clusters before running the clustering algorithms. 

In **Hierarchical Clustering**, clusters are built in a hierarchy (wow). 
- Hierarchy of clusters is represented as a tree (or **dendrogram**).
- Root of tree is the **universe** cluster
	- It includes all data records
- Leaves form *single-point* clusters.
	- These include individual data records from each leaf. 
- From leaves to root, the most similar "single-point" clusters are combined to form larger clusters.
	- This process is repeated until reaching the *universe* cluster.

There are two types of hierarchical clustering:
- Agglomerative
	- bottom-up approach
	- starts at the *single-point* clusters and moves up by merging similar clusters until it reaches the *universe* cluster.
- Divisive
	- Top-down approach

Details and steps of the **agglomerative** clustering algorithm:
1. Consider each data record as a cluster.
	1. number of clusters equal to $n$, the number of data records.
2. Merge the two closest cluster into one bigger cluster.
	1. number of clusters becomes $n-1$
3. Repeat step two until a single cluster is formed (the *universe* cluster).
4. Construct a tree (i.e., dendrogram) to visualize the progression of the formed clusters at each step. 

The instructions are to merge 'clusters' into each other, is this based on the centroid?

To determine if clusters are close to each other we use the concept of *proximity matrix*. A **proximity matrix** includes all the distances from one data record to the other data records. 
- It is therefore an $n \times n$ matrix of distances.
- The minimum off-diagonal value in this matrix defines the closest data records.
- Distances can be Euclidean, Manhattan, or any other suitable distance measure
	- Just be consistent.

When cluster contain more than one data record, we have options to determine distances:
- Determine distances between closest points of the two clusters
	- Called **single linkage**
- Determine distance based on arithmetic means of the distances between the objects of these two clusters.
	- Called **Average Linkage**
- Determine distance between the farthest points of these two clusters.
	- Called **Complete Linkage**

Example given on page 49 of course book with a small 2D dataset, made up students with grades in maths and physics. 
- The Euclidean distances is the square-root of the sum of squared differences.
- Develop a proximity matrix
	- The Diagonal is 0 because that is distance from self. 
	- matrix is symmetrical along the diagonal. 

The Dendrogram has distance on Y-axis with entities on the X-axis. The entities merge as we increase distance. Dendrogram is very important visualization tool:
- Shows how clusters progress from the *single-point*  cluster to the *universe* cluster.
- Aids the decision for the optimum number of clusters in the given dataset. 

To determine the optimum number of clusters to ensure the largest intra-distances, follow these steps:
1. Determine the largest vertical line in the dendrogram that does not intersect any of the other clusters. (Max distances no merges took place)
2. Draw a horizontal line along this line.
3. Optimal number of clusters is equal to the number of intersections this horizontal line has!

[Hierarchical Clustering | Geeks For Geeks](https://www.geeksforgeeks.org/machine-learning/hierarchical-clustering/):
- This provides a good example

[Hierarchical Clustering | Wikipedia](https://en.wikipedia.org/wiki/Hierarchical_clustering):
- Lists the formulas for this

### 2.3.1 Hierarchical Clustering in Python

p. 53

The book runs the algorithm over a dataset of customers of a whole-sale distributor. 

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import scipy.cluster.hierarchy as shc
from sklearn.cluster import AgglomerativeClustering

data = pd.read_csv('Wholesale customers data.csv')
data.head()

#Normalize the dataset to get all the features at the same scale
from sklearn.preprocessing import normalize
data_scaled = normalize(data)
data_scaled = pd.DataFrame(data_scaled, columns=data.columns)
data_scaled.head()

# Draw the dendrogram to find the optimum number of clusters
plt.figure(figsize=(10, 7))

plt.title("Dendrograms")
Text(0.5, 1.0, 'Dendrograms')
dend = shc.dendrogram(shc.linkage(data_scaled, method='ward'))
plt.show()

# Very cool plot is displayed
# We can see optimum number of clusters equals 2

# apply hierarchical clustering for two clusters only
cluster = AgglomerativeClustering(n_clusters=2,
affinity='euclidean', linkage='ward')
cluster.fit_predict(data_scaled)
# If you print the array that is fit it has 0-1
# where “0” implies a customer in the first cluster, and “1” implies
# a customer in the second cluster.

# to visualize the two clusters
plt.figure(figsize=(10, 7))
plt.scatter(data_scaled['Milk'], data_scaled['Grocery'], c=cluster.labels_)
plt.show()
```

### 2.3.2 Limitations of Hierarchical Clustering

p. 56

Hierarchical clustering is easy to implement and can be more informative than the unstructured set of flat clusters returned by most other clustering approaches. 

It is also easier to decide on the number of cluster by looking at the formed tree (i.e.; dendrogram). 

The most important value is the lack of assumptions concerning a particular number of clusters in the beginning of the algorithm. 

Drawbacks:
- Once a decision is made to combine two clusters, it cannot be undone. 
	- Cannot undo previous steps.
- Not suitable for large datasets.
- Very sensitive to outliers within data.
- Alternative for large datasets, k-means is typically faster and produces tighter clusters. 

## 2.4 Density-Based Clustering

p. 57

**Centroid-Based** clustering algorithms do not address the fake outliers.
- These data records still get assigned to clusters even if they do not belong in any. 

**Density-based** clustering approaches work to identify clusters by grouping "dense" data records together. This permits the representation of arbitrarily shaped clusters.

The estimation of "dense" clusters is based on the **neighborhood concept**. 
- The $\varepsilon$-neighborhood of record $p$ is the set of points contained in a shape of extension $2 \varepsilon$, centered at $p$.  
- Assuming Euclidean distance
	- Surface is a circle for 2D space, Sphere in 3D space, and $N$-sphere for general multi-dimensional space. 

Generally, the $\varepsilon$-neighborhood of a point $p$ in dataset $d$ is given by:

$$
N(p) = \left\{ q \in d \ | \ \text{dist}(p,q) \le \epsilon \right\}
$$

The number of data points in $N(P)$ indicates how dense the $\varepsilon$-neighborhood at $p$ is. 

We define a minimum density value of MinPts for a neighborhood to be considered part of a cluster. 

These definitions leads to three possible descriptions for the data record at $p$:
- Core point
	- Record is core point if its $\varepsilon$-neighborhood contains more than the specified MinPts.
- Border point
	- Record is this if the $\varepsilon$-neighborhood has fewer than the specified MinPts, but the point is in the $\varepsilon$-neighborhood of a core point. 
- Noise point (outlier)
	- If neither Core nor Border.

### 2.4.1 DBSCAN Algorithm

p. 57

Technique proposed to perform the general **Density-Based Spatial Clustering for Applications with Noise** (DBSCAN). It is efficient for large datasets of thousands of records yet requires some domain knowledge of the underlying datasets. 

Steps for DBSCAN algorithm:
1. Assume MinPts and the surface radius ($\varepsilon$).
2. Start at arbitrary data record ($p$).
3. If $p$ contains MinPts within its $\varepsilon$-neighborhood, cluster formation starts. Else, $p$ is labeled as noise. This may be modified later if $p$ is found within $\varepsilon$-neighborhood of core point data record.
4. Density-connected cluster step:
	1. if $p$ is a core point
		1. Then data records within its $\varepsilon$-neighborhood are part of the formed cluster.
	2. All of these data records are added, along with their own $\varepsilon$-neighborhood, if they are also core points.
5. Start a new data record (not previously processed), and repeat steps 3 to 4 until there are no unhandled records.

### 2.4.2 DBSCAN in Python

p. 58

Example in Python with randomly generated dataset. 

```python
import numpy as np
from sklearn.cluster import DBSCAN
from sklearn import metrics
from sklearn.datasets.samples_generator import make_blobs
from sklearn.preprocessing import StandardScaler
from pylab import *
import matplotlib.pyplot as plt

# Generate sample data
centers = [[1, 1], [-1, -1], [1, -1]]
X, labels_true = make_blobs(n_samples=750, centers=centers, cluster_std=0.4, random_state=0)

# Scale and standardize the dataset
X = StandardScaler().fit_transform(X)
xx, yy = zip(*X)
scatter(xx,yy)
show()

# Set up DBSCAN parameters
db = DBSCAN(eps=0.3, min_samples=10).fit(X)
core_samples = db.core_sample_indices_

core_samples_mask = np.zeros_like(db.labels_, dtype=bool)
core_samples_mask[db.core_sample_indices_] = True
 the number of clusters
n_clusters_ = len(set(labels)) - (1 if -1 in labels else 0)
# n_clusters_ = 3

labels = db.labels_
# labels is array of { -1, 0, 1, 2 }
# if the label equals “-1”, this means the data record is an outlier.
# find the outliers
outliers = X[labels == -1]

print(outliers)
# >>> array of points

# Get the contents of each cluster
cluster1 = X[labels == 0]
cluster2 = X[labels == 1]
cluster3 = X[labels == 2]

# Plot the results with a specific color for each cluster, and a black color for the noise points
unique_labels = set(labels)
colors = ['y', 'b', 'g', 'r']
for k, col in zip(unique_labels, colors):
	if k == -1:
		col = 'k'

class_member_mask = (labels == k)
xy = X[class_member_mask & core_samples_mask]
plt.plot(xy[:, 0], xy[:, 1], 'o', markerfacecolor=col, markeredgecolor='k', markersize=6)
xy = X[class_member_mask & ~core_samples_mask]
plt.plot(xy[:, 0], xy[:, 1], 'o', markerfacecolor=col, markeredgecolor='k', markersize=6)
plt.title('number of clusters: %d' %n_clusters_)
Text(0.5, 1.0, 'number of clusters: 3')
plt.show()
```

If you change the "eps" and the "MinPts" values, you get different cluster configurations. 

### 2.4.3 Limitations of DBSCAN

p. 64

An important advantage of DBSCAN is no requirement to estimate the number of clusters in the beginning of an algorithm. It can infer the number of clusters 
according to the underlying dataset. 

It also discovers arbitrarily shaped clusters. 

This technique efficiently separates clusters of high density versus clusters of low density within a given dataset, while pragmatically handling the contained outliers. 

However:
- If the dataset has records that form clusters of varying density;
	- Then DBSCAN fails to perform as effectively;
	- Because $\varepsilon$ and MinPts params cannot be chosen separately for each of the clusters.
- If the dataset and its involved features are not well understood by a domain expert;
	- Then setting up $/varepsilon$ and MinPts could be tricky.
	- And this could lead to needing comparison of several iterations with different param values. 

## Summary

p. 65;

**Clustering Analysis** is an unsupervised learning tool that helps the data analyst to infer data-driven patterns that may warrant further investigation, without the need for labeled outcomes. 

Major clustering methods are:
- Centroid-based clustering
- Gaussian mixture models clustering
- Hierarchical clustering
- Density based clustering
