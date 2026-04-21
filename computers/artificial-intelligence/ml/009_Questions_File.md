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



# Unit 5. Decision Trees

Q.) What is a decision Tree?

> [!Answer]-
> TODO

Q.) How do you use a decision tree in supervised learning?

> [!Answer]-
> TODO

Q.) What are the different approaches for constructing a Decision Tree?

> [!Answer]-
> TODO

Q.) What are the different types of feature-ranking techniques used in Decision Trees?

> [!Answer]-
> TODO

Q.) What is the purpose of the different feature-ranking techniques?

> [!Answer]-
> TODO

Q.) What is meant by Tree Pruning?

> [!Answer]-
> TODO

Q.) When does Tree Pruning Occur?

> [!Answer]-
> TODO

Q.) How do tree classifiers help in building up an ensemble model?

> [!Answer]-
> TODO

## Introduction

Q.) What do decision trees represent?

> [!Answer]-
> A group of classification techniques that are based on the construction of a tree like structure. 

Q.) What does the tree like structure of a decision tree represent?

> [!Answer]-
> The tree structure represents a set of nested decisions that make use of the provided feature information in a sequential manner to categorize the input object. 

Q.) Decision Tree classifiers are widely used in various fields, name the two we talk about.

> [!Answer]-
> Image processing and character recognition.

Q.) Name the 6 different areas of application we mention in the course book.

> [!Answer]-
> Medicine, financial analysis, astronomy, manufacturing, production, molecular biology. 

## 5.1. Introduction to Decision Trees

Q.) To which learning paradigm do Decision Trees belong?

> [!Answer]-
> They are classifiers and belong to the field of Supervised Learning.

Q.) How many steps are there for building a decision tree? How are they referred to (names)?

> [!Answer]-
> There are two steps: the learning step and the decision step. 

Q.) Provide a high-level description of the steps to build a decision tree.

> [!Answer]-
> The Learning step is the induction of a tree structer based on the training data of labeled data instances. 
> The decision step includes the classification of testing data on non-labeled instances. 

Q.) How is each instance in a dataset characterized?

> [!Answer]-
> By its set of features.

Q.) What makes up the structure of a constructed decision tree?

> [!Answer]-
> Decision nodes, branches, and leaves. 

Q.) What does each internal node in the decision tree represent?

> [!Answer]-
> A decision based on a feature!

Q.) How are branches of the Decision node selected? 

> [!Answer]-
> Based on the value of the feature. 

Q.) What do the branches in the decision tree represent?

> [!Answer]-
> Each branch represents a conditional statement (if-condition). 

Q.) What does the root node of the decision tree represent?

> [!Answer]-
> It represents the most important feature of the data  objects with respect to the classification problem at hand.

Q.) What is a **Discrete Feature**?

> [!Answer]-
> A "discrete feature" is a property of a certain value whose value has a finite set of distinct values. I like to think finite and countable. 

Q.) What is a **splitting attribute**?

> [!Answer]-
> It is a feature represented **at** an internal node. The feature that determines how splitting occurs. It is the feature that the decision node uses to make a decision. Think of it like the content of the node. 

Q.) What is a "decision node"?

> [!Answer]-
> The internal node that represents a feature. It is a point in the tree where a decision will be made, a fork in the road. 

Q.) What is the "splitting criterion"? 

> [!Answer]-
> This is the condition to check, on a branch, that leads us to the next decision node. 

Q.) What is a "ranking technique" and when would one be needed?

> [!Answer]-
> A ranking technique helps detect the degree of importance of a feature to a given classification problem. They are required when a dataset contains more than one feature. 

Q.) How do you use a ranking technique when building a decision tree?

> [!Answer]-
> The classifier uses the technique to rank feature in terms of importance. Then, the classifier selects the most salient feature for representing the root node and then the remaining features in decreasing importance for the rest of the tree nodes. 

Q.) What is a **decision rule**?

> [!Answer]-
> It is a group of conditions that enable the classifier to determine the class membership of an instance.

Q.) Why is the visual form of a decision tree important to experts of a domain problem?

> [!Answer]-
> Visualizing the set of decision rules allows experts of the domain problem to understand the reason for classifying the instances. 

Q.) What is the relationship between the number of decision rules and the number of training instances.

> [!Answer]-
> They grow together, as you need more decision rules, you also should have more training instances. 

Q.) What is the relationship between complexity of the decision rules and the number of features?

> [!Answer]-
> As the number of features increases, so does the complexity of the decision rules.

Q.) What is the relationship between complexity and visual understanding?

> [!Answer]-
> Induction of a complex decision tree reduces the advantage of interpreting its visual form. 



Q.) What is the main concern of increasing the decision complexity?

> [!Answer]-
> As you add more decision rules the growing concern is that the tree begins to fit too closely to a specific set of instances, leading to overfitting. 

Q.) How does overfitting occur in a decision tree?

> [!Answer]-
> Too many decision rules, too much complexity and overtraining.

Q.) What happens when overfitting occurs to a decision tree

> [!Answer]-
> The decision tree loses its ability to classify new data instances. 

Q.) What happens if the classifying model is not trained enough, the decision tree classification model?

> [!Answer]-
> The decision tree will be too simple to classify instances accurately, causing underfitting, the opposite of overfitting. 

#here -> Top of 111.

Q.) Describe what a successfully accurate decision tree is able to do.

> [!Answer]-
> A successfully accurate decision tree is a classifying model that has the ability to generalize, which avoids both overfitting and underfitting. 

Q.) When is the inferred decision tree most effective?

> [!Answer]-
> When it correctly covers as many instances in the training dataset as possible without overfitting. 

Q.) What is a problem decision trees may have while building the tree?

> [!Answer]-
> Decision trees may include branches that represent outliers or noise in the input dataset. 


Q.) How do decision tree classifiers overcome issues to improve classification accuracy?

> [!Answer]-
> They commonly apply some pruning methods to remove branches based on outliers and noise to improve classification accuracy. 

Q.) What is the engine behind the success of decision tree classifiers (not a real engine)? Maybe, what ability drives success of a decision tree classifier?

> [!Answer]-
> The success is driven by their ability to encode decision-making knowledge in the form of decision rules.

Q.) Why are decision trees easier to understand and interpret compared to other classifiers like SVM and neural networks?

> [!Answer]-
> The trees are constructed in a way that enables the analyst or decision maker to understand the reason for classifying a tested instance in a particular way; they are easier to interpret due to their natural representation. The other classifiers are black box classifiers, the decision logic is unknown. 

Q.) What are two advantage of a decision tree classifier that relate to mathematics?

> [!Answer]-
> Their independence on statistical distribution of the input data and their ability to deal with input datasets where the relationship between the features and class labels of the associated objects is nonlinear. 


## 5.2. Decision Tree Approaches for Classification

Q.) What are the most popular decision trees?

> [!Answer]-
> ID3 (Quinlan, 1896), C4.5 (Quinlan, 1993), and CART (Breiman et al., 1984). 

Q.) How do different approaches differ from each other?

> [!Answer]-
> They differ in the way that features are ranked and selected while creating the decision tree, and with respect to the utilized pruning mechanism. 
> 1.) feature ranked;
> 2.) feature selected;
> 3.) pruning technique.

Q.) What are popular feature ranking techniques used in decision tree approaches?

> [!Answer]-
> 1.) Information Gain
> 2.) Gain Ratio
> 3.) Gini Index

Q.) Please map the popular decision trees to their respective feature ranking technique.

> [!Answer]-
> 1.) ID3     ->  Information Gain
> 2.) C4.5   ->  Gain Ratio
> 3.) CART ->  Gini Index

Q.) What does ID3 really stand for?

> [!Answer]-
> Iterative Dichotomiser.

Q.) How does ID3 use Information Gain?

> [!Answer]-
> ID3 uses IG to select the best splitting features!

Q.) What is a high-level overview of the Information Gain feature-ranking technique?

> [!Answer]-
> IG characterizes the distribution of the class data in a feature vector. It measures the degree of homogeneity of the classes induced by a decision node (i.e., a split of feature values). 
> The calculation of the IG dataset features is based on measuring the **entropy** of the class assignments with respect to a split in that feature. 
> This quantity is inversely proportional to IG. 
> I.E. IG is the reduction of entropy of class assignment based on the feature split under examination.

Q.) What is Entropy?

> [!Answer]-
> Generally speaking, "entropy" is the degree of disorganization and randomness in a set of observations. 

Q.) What is the calculation of information gained from a feature based on?

> [!Answer]-
> It is based on the calculation of its Entropy. 

Q.) Examples; describe the entropy of 3 datasets:
1. Objects in dataset are equally divided between two existing classes.
2. Objects in dataset are more of one class than another.
3. Objects in dataset are all of one class type.

> [!Answer]-
> 1.) Entropy is One because the dataset is completely heterogeneous.
> 2.) Entropy is $> 0$ but $< 1$ because the impurity has decreased (compared to 1).
> 3.) Entropy is Zero because the dataset is completely homogenous. 

Q.) What is the Entropy of a dataset $D$ in mathematical representation?

> [!Answer]-
> ...

$$
\tag{1}
\mathbf{Info}(D) = \sum_{k=1}^m{
\left(
-P_k \cdot \log(P_k)
\right)
}
$$

Where:
- $D$ is the dataset of instances.
- $k$ is a class.
- $P_k$ is probability that any instance belongs to a particular class.

The probability is calculated as the ratio between the number of instances that belong to $k$ and the total number of instances in $D$. 

Q.) After the first partition, how do we represent instances that are partitioned by a feature $f$? 

> [!Answer]-
> ...

$$
\begin{align}
\tag{2}
\mathbf{Info}_f(D) &= \sum_{i=1}^v{
\left(
\frac{|d_i|}{|D|} \cdot \mathbf{Info}(d_i)
\right)
} \\
\mathbf{Info}_f(D) &= \sum_{i=1}^v{
\left(
\frac{|d_i|}{|D|} \cdot 
\left(
\sum_{k=1}^m{
\left(
-P_k \cdot \log(P_k)
\right)
}
\right)
\right)
}
\end{align}
$$

Where:
- $D$ is the dataset of instances.
- $f$ is the feature of partition. 
- $k$ is a class.
- $P_k$ is probability that any instance belongs to a particular class.

This function measures the ability of any *feature to split* the dataset into equally divided partitions! Each partition corresponds to a single class label. 

A feature $f$ partitions the instances in the dataset into $v$ subsets, considering that this feature is of $v$ distinct values. The instances in each subset $d_i$ have the same value of the feature $f$. 

The function $\mathbf{Info}_k(D)$ is calculated as the weighted sum of the entropy of the $v$ subsets.

Q.) In the partitioned information gain function, $\mathbf{Info}_f(D)$, please explain the representation of $\mathbf{Info}(d_i)$.

> [!Answer]-
> ...

$\mathbf{Info}(d_i)$ represents the **entropy** of *subset* $d_i$. 

The term $|d_i|/|D|$ acts as the weight of this partition $d_i$. 

The value of $|d_i|$ is the number of instances in partition $i$.

The value of $|D|$ is the total number of instances in the dataset.

Q.) When do we reduce the entropy ($\mathbf{Info}(D)$) in dataset $D$ to ($\mathbf{Info}_f(d_i)$)?

> [!Answer]-
> When the feature $f$ splits the instances in $D$. 

Q.) What is a reduction in entropy caused by?

> [!Answer]-
> Reduction in entropy due to a specific feature is equivalent to the information gain of the feature. 

Q.) Mathematically define the information gain of feature $f$.

> [!Answer]-
> ...

$$
\tag{3}
\mathbf{Gain}(f) = \mathbf{Info}(D) - \mathbf{Info}_f(D)
$$

Q.) How is information gain of a feature related to the entropy of a dataset?

> [!Answer]-
> The information gain of a feature is inversely proportional to entropy of the dataset when the feature is used.
> The feature divides the dataset into a group of subsets. 
> If all values of the feature are distinct, then each subset includes only ONE instance.

Q.) Is information gain able to be calculated for discrete and continuous features?

> [!Answer]-
> No, only discrete features. 

#here p. 113; C4.5 and Gain Ratio
