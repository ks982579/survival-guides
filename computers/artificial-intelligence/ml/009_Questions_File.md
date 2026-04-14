# Unit 1

1.) What is Machine Learning?

<details>
    <summary>Answer</summary>
    Machine learning is a method of data analysis that automates analytical model building. This branch of artificial intelligence is based on the idea that machines are able to learn and adapt through experience.
</details>

2.) Please define classification and give an example.

What: A form of supervised ML. 
How: Assigns objects to one of a set of predefined classes. 

In classification, one assigns objects (instances) to one of a set of predefined classes designated by class labels. This is done based on information extracted from the training data that has already been classified. Classification is a form of supervised machine learning. Example: Determine if a given e-mail is a spam.

Classification is a form of supervised learning. It performs classification by mapping objects to a set of predefined classes, designated by a class label. This is done based on information extracted from training data that has already been classified. 

An example would be an e-mail spam filter.

3.) List 3 examples of classification algorithms.

K-Nearest neighbor

Decision trees

Bayesian classifier

4.) What are evaluation metrics in a classification algorithm. 

Metrics usually come from confusion matrix. You have Accuracy, precision and recall. There is also the F-score, a weighted average of precision and recall. 

A: The confusion matrix is used to evaluate the model. Some of the metrics that are based on the confusion matrix are: accuracy, precision, recall, and f-score.

Well done!

2.) What are the 3 ingredients of ML? (P.E.T.).

3.) How is ML different from Traditional Programming?

4.) How does ML transform data into information?

5.) What are applications of ML? (Unit 2 of AI Course).

6.) What are the 4 paradigms of ML?

7.) What is a training dataset?

8.) What is a Testing dataset?

9.) What is a confusion matrix?

10.) How do you determine the best ML approach/solution for a problem?

11.) What is the trade-off between goodness of fit and complexity of the model?

12.) How do you generally improve predicitive performance?

13.) What is overfitting? Why does it happen and how does it impact your model?

14.) What does an efficient ML model do?

15.) Give a brief explanation of the Supervised Learning paradigm. 

16.) What is the objective of Supervised learning?

17.) What happens to parameters of model during the learning process?

They are updated until the optimum setting is achieved.

18.) What governs the parameter updating process during learning?

A specific loss function.
The objective becomes adjusting parameters to minimize the loss function. 

19.) What is typical loss function of regression?

The MSE.

20.) What is the typical loss function for classification problems?

Can be the number of wrongly classified instances. 

21.) What is the structure of the supervised learning procedure?

instances of training set are used to learn the model via classification/regression algorithm.
Then, modle is applied to predict the otupt for testing samples (not presented during model's training. 

22.) What type of Supervised learning would be applied to determine the current value of a home?

23.) Know Supervised learning techniques on page 22-23.

24.) What is unsupervised learning, when do we use?

The objective is to develop ML models to discover patterns and structures in training data. 

25.) What is "Dimensionality Reduction"?

the process of removing the irrelevant variables form the dataset. 

26.) What is an outlier?

27.) what are True and Fake outliers?

28.) What are Unsupervised Learning Techniques (page 25.)?

29.) What is Reinforcement Learning?

30.) What are the ingredients of Reinforcement Learning?

A.A.E.S.R.P.V.

31.) What are applications of Reinforcement Learning?

Games and robotics. 


# Unit 2. Clustering

1.) What is Clustering?

To gather data records into natural groups of similar samples according to predefined similarity / dissimilarity metrics. 
This results in extracting a set of useful information about the given dataset. 

2.) Name some examples that utilize clustering.



3.) What are 4 different types of Clustering methods?

Centroid-based; Gaussian Mixtures Models; Hierarchical; Density-based

4.) What is "high intra-cluster similarity"?

When the contents of a cluster are similar to each other. 
Contents of cluster should be similar to each other, they should have high intra-cluster similarity. 

5.) What is "high inter-cluster separation"?

When the contents of clusters are very different (dissimilar) from the contents of other clusters. 
Again, resulting clusters from a cluster analysis should have high inter-cluster separation. 

6.) What 2 properties should clusters have as a result from cluster analysis?

Clusters should have both high intra-cluster similarity and hight inter-cluster separation. 

7.) What are two commonly implemented simple forms of distance functions? 

Euclidean distance.
Manhatten distance.

8.) What is the formula for Euclidean distance for two dimensional datasets?

9.) What is the formula for the Manhattan distance?

10.) What is a "Feature"?

A measurable and observable quantity about the data record. 

11.) What step should be done to features of the datasets that have scales with widely differing ranges?

Feature scaling - Standardize the ranges to the same scale before progressing in any form of clustering analysis. 

12.) How do we evaluate clustering results? 

Usually evaluation is completed by Manual Inspection of results,
benchmarking on existing labels, and distance measures to denote similarity level
within a cluster and dissimilarity level across clusters. 

13.) What is "Clustering Analysis"?

This type of unsupervised Learning sorts a set of data records into clusters, or groups. 

14.) What fields apply clustering analysis?

pattern recognition, image processing, spatial data analysis, bioinformatics, crime analysis,
medical imaging, climatology, and robotics. 

15.) What is the noteworthy area of clustering application?

Market segmentation, which focuses on grouping customers into clusters of different characteristics,
and using them for targeted marketing. 

Another common application is to implement clustering analysis to develop a recommendation system. 

16.) What are the 4 main methods / techniques of clustering analysis we discuss in the book?

Centroid-based clustering methods;
Gaussian mixtures models clustering methods;
Hierarchical Clustering methods;
Density based clustering methods. 

17.) What is a Centroid?

18.) What is Centroid-Based Clustering? give a brief explanation (high-level) of how it works.

Centroid-based clustering searches for a pre-determined number of clusters within an unlabeled and possibly multidimensional dataset. 

The rule is that the distance between a data record and each of the cluster's centroids is calculated and the data record is assigned to the cluster achieving the minimum distance. 

19.) How many clusters can a data record be assigned to in centroid-based clustering?

One and only one. 

20.) What is k-means clustering?

It is a centroid-based clustering approach commonly used in practice. 

This method partitions $n$ data records from the given dataset into (k) clusters. 

21.) What are the three main steps for K-means clustering?

- Initialization
	- A number of clusters are assumed (K is predetermined).
	- The centroid of each cluster is randomly defined.
- Assignment
	- Clusters are formed by connecting each data record with nearest centroid. 
- Update
	- A more accurate centroid of each cluster is calculated as the mean point of its included data records. 
- REPEAT assignment and update steps until convergence, when no changes in the calculated clusters' centroids. 

22.) What is a simple procedure to define the initial placement of a cluster's centroid?

To locate it at one of the given data records. It is PRUDENT to locate the centroids FAR from each other to span the whole domain of data records. 

23.) What are some advantages of the K-means clustering?

page 41. 

- Simple to employ;
- Suitably efficient for large datasets;
- Assures convergence;
- Easily assume initial centroids' placement;
- Smoothly adjusts the clusters' oulines when new data records are introduced.

24.) What are some limitations of K-means clustering?

- Determining number of clusters - significantly difficult to predict. 
- Different initial partitions can result in different final clusters. 
- Assumes spherical shape of clusters
	- technique does not work effectively in clustering datasets having regions with differently shaped densities. 
- Handles only numerical datasets.
- initial assumptions of controids may result in poor convergence rate.
- Normalization of dataset may produce completely different results. 
- K-means with standard Euclidian distance is not well-suited for high-dimensional data.
- If dataset is dynamic over time, adds burden of checking optimum number of clusters periodically.
- Fake outliers may not be detected and influence structures of clusters. 

A lot.

25.) What is the computation complexity of the distance calculation in k-means clustering?

With $M$ iterations, and computation distance of $n$ records, and centroids $K$, the computation complexity is $O(M \cdot n \cdot K)$. 

26.) What is a "Probabilistic Generative Model"?

Models that explain how input data are generated in terms of their joint probability distributions. Each data record has a probability for belonging to each cluster and is assigned to a cluster returning the highest probability. 

27.) What shape does "hard" clustering genearte?

Circular clusters centered at the found centroids. 

28.a.) What is a Gaussian Mixture Model?

It is a probabilistic generative model that represents data as a combination of several Gaussian distributions, each with its own mean and variance, weighted by a mixing coefficient. Each distribution represents its own cluster. 

Book answer: defined as a set of $K$ probability distributions and each distribution corresponds to one cluster. 

28.b.) What a Gaussian Mixture Models commonly used for? (2 answers).

Clustering and density estimations. 

28.) How does one determine the number of clusters for a GMM?

GMM initially assumes the number of clusters for the input dataset. 

29.) Does a GMM ever take circular shapes like k-means? If so, when?

The GMM centroids are controlled by $\mu$ and $\sigma$ parameters. In the particular case when the inferred GMM clusters have equal and diagonal covariance matrix, they look equivalent to results obtained by k-means clustering. 

30.) What is the "task" for GMM clustering?

p. 43;

31.) How to GMM achieve it's task?

Implements the expectation maximization algorithm. 

32.) What is the "expectation maximization (EM) algorithm"? 

It is an iterative method to find the maximum likelihood estimates of parameters $\mu$ and $\sigma$ to get the "best fit" model for input dataset. 

Iteration stops when desired convergence criterion is achieved. 

33.) When do we implement the EM algorithm?

Implemented when there is an analytic model for the dataset and the model's shape is known, but parameters $\mu$ and $\sigma$ of the model are not known. 

34.) What steps are in the EM algorithm?

The EM algorithm alternates between 2 steps:
- Expectation (E)
- Maximization (M)

1.) First - assume number of cluster $K$. 
Guess initial parameter values for each cluster:

$$
\mu_k, \sigma_k, k= 1, \dots, K.
$$

Assume a weight for each cluster (i.e. probability any given record is a member of specific cluster) $q_k$. 

2.) Now the E-step:

Compute membership probability for each data record... formula p. 43;
Construct expression for likelihood of all data records... p. 44;

3.) The M-step:

For each cluster $k$, calculate total likelihood $m_k$:

$$
\begin{align}
m_k = \sum_{i=1}^n r_{i,k} \\
k = 1, \dots, K
\end{align}
$$

Then update the initially assumed parameters:

$$
\begin{align}
q_k^{\prime} &= ... \\
\mu_k^{\prime} &= ... \\
\sigma_k^{\prime} &= ...
\end{align}
$$

4.) Iterate through steps E and M (2 and 3) until no further changes in parameters are required / noted. Or, when the log-likelihood function converges:

$$
\sum_{i=1}^N 
{\left( 
	\ln 
	{\left(
		\sum_{k=1}^K
		{\left(
			q_k^{\prime} \cdot P(x_i k)
		\right)}
	\right)}
\right)}
$$

5.) Assign each data record to the cluster where it has the highest membership probability. 



35.) What is a natural initial assumption for cluster weights, $q_k$?

$$
\sum_1^K {q_k}  =1
$$

All weights are equal for all clusters. 

36.) How do you use Gaussian Mixture model in Python?

```python
from sklearn.mixture import GaussianMixture

gmm = GaussianMixture(n_components = 3)
gmm.fit(d) # d is pd.DataFrame
labels = gmm.predict(d) # predict cluster
gmm.means_ # final means of each cluster
```

37.) Advantages of GMM clustering?

It is preferred for datasets consisting of regions that do not look like simple circles, maybe more like ellipsoids.

It is desirable to know the probability of a data record to belong to each cluster.

It is able to simultaneously optimize a large number of variables to create both:
- "hard" cluster with crisp 0-1 membership encoding, and
- "soft" clusters with soft borders according to the probability level of each data record.

38.) What are some limitations of GMM Clustering?

The EM algorithm can be slow because time consuming to find probability distribution for each data record. 

It can get stuck in a local maximum of log-likelihood functions. 

The steps suffer from heavy computations of conditional probabilities. 

> So, slow and expensive to run with a chance of incorrect results. 

39.) Compared to K-Means clustering, what challenge does hierarchical clustering solve?

It solves the challenge of deciding the number of clusters to use during the initialization of K-means clustering. 

40.) What is a Dendrogram

https://www.displayr.com/what-is-dendrogram/

A dendrogram (or clustering dendrogram) is a diagram that shows the hierarchical relationship between objects.

https://en.wikipedia.org/wiki/Dendrogram

A diagram representing a tree graph. 

https://www.geeksforgeeks.org/python/scipy-cluster-hierarchy-dendrogram/

A Dendrogram is a tree-like diagram used to visualize the relationship among clusters.

41.) What do we call the root of the tree?

The "Universe" cluster.

42.) What is the tree's "Universe"?

It is the root of the tree that includes all data records.

43.) What are tree leaves called in a Dendrogram?

These form "single-point" clusters, just an individual data record. 

44.) What are the two types of hierarchical clustering?

Agglomerative and Divisive. 

45.) What is Agglomerative Clustering?

Clustering is done bottom-up approach, starting at "single-point" clusters and moves up by merging similar clusters until it reaches the "Universe" cluster. 

46.) What is Divisive clustering?

Clustering is done in a top-down approach. 

47.) What are the steps of the agglomerative clustering algorithm?

1.) Consider each record as a single-point. The number of clusters is equal to $n$, which is the number of data records. 

2.) Merge the two closest clusters into a bigger cluster. You now have $n-1$ clusters.
- requires calculations of distances.

3.) repeat step two until you have a single cluster, the "Universe" cluster.

4.) Construct a tree (i.e. dendrogram) to visualize the progression of the formed clusters at each step.


48.) How do you know if two single-point clusters are close to each other?

Use a proximity matrix. - includes all distances from records to each other. 
- can use Euclidean, Manhattan, or another distance measure.

49.) How to measure distance in Hierarchical clustering when a cluster has more than one record. 

Your options are:
- Single Linkage - determine distance based on closest points of clusters.
- Average linkage - like centroids, with averages.
- Complete linkage - distance between farthest points of clusters. 

50.) Why is Dendrogram important?

- Visualization of hierarchical clustering algorithm.
- Aids in decision of optimum number of clusters in dataset. 
	- greater the length of vertical lines, more distance between clusters. 

51.) What is optimum number of clusters for hierarchical clustering?

The optimum number of clusters, which ensures the
largest intra-distances, can be determined heuristically through the following steps:
- Determine the largest vertical line in the dendrogram that does not intersect any of the other clusters. In our example, it is the vertical line from 9.43 to 14.14 with a length of 4.71.
- Draw a horizontal line along this line.
- The optimal number of clusters is equal to the number of intersections this horizontal line has. In our example, there are two intersections, as shown below.

52.) What are advantages of Hierarchical Clustering?

Easy to implement.
Results are more informative than unstructured set of flat clusters returned by most other clustering approaches. 
Easier to decide number of clusters. 
Lack of assumptions concerning a partiuclar number of clusters in initialization!

53.) What are limitations of Hierarchical Clustering?

Once decision is made to combine two clusters, that cannot be undone. 
Not suitable for large datasets.
Sensitive to outliers within data. 

Use k-means over hierarchical clustering for large datasets. 

... 2.4 is Density Based but I am out of steam...

p. 57;


# Unit 3. Regression


# Unit 4. Support Vector Machines
