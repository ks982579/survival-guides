# Unit 1

> [!question]
> 1.) What is Machine Learning?

> [!answer]-
> Machine learning is a method of data analysis that automates analytical model building. This branch of artificial intelligence is based on the idea that machines are able to learn and adapt through experience.
> It is a mathematical and algorithmic approach to problem solving.
> It is devoted to understanding and building methods that "Learn".
> Methods leverage data to improve performance on some set of tasks.

> [!failure]



> [!question]
> What is "Machine Learning" in simple terms of performance, experience, and tasks?

> [!answer]-
> Machine learning is a field of study concerned with the question of how to construct computer programs that automatically improve their performance (P) from experience (E) with respect to some provided tasks (T). 

> [!failure]



> [!question]
> 2.) Please define classification and give an example.

What: A form of supervised ML. 
How: Assigns objects to one of a set of predefined classes. 

In classification, one assigns objects (instances) to one of a set of predefined classes designated by class labels. This is done based on information extracted from the training data that has already been classified. Classification is a form of supervised machine learning. Example: Determine if a given e-mail is a spam.

Classification is a form of supervised learning. It performs classification by mapping objects to a set of predefined classes, designated by a class label. This is done based on information extracted from training data that has already been classified. 

An example would be an e-mail spam filter.

> [!question]
> 3.) List 3 examples of classification algorithms.

> [!answer]
> - K-Nearest neighbor
> - Decision trees
> - Bayesian classifier


> [!question]
> 4.) What are evaluation metrics in a classification algorithm. 

> [!answer]-
> Metrics usually come from confusion matrix. You have Accuracy, precision and recall. There is also the F-score, a weighted average of precision and recall. 
> A: The confusion matrix is used to evaluate the model. Some of the metrics that are based on the confusion matrix are: accuracy, precision, recall, and f-score.



> [!question]
> 2.) What are the 3 ingredients of ML? (P.E.T.).

> [!answer]
> Performance, Experience, and Task.



> [!question]
> 3.) How is ML different from Traditional Programming?

> [!answer]-
> Traditional programming constructs explicit processing of input variables into desired outputs via a set of code instructions. 
> Machine learning uses mathematical and algorithmic approaches to generate a model that performs the mapping based on a set of data that includes inputs and output values. 
> ML builds models based on sample data to make predictions or decisions without explicit programming. 

> [!failure]



> [!question]
> 4.) How does ML transform data into information?

> [!answer]
> ML algorithms build models based on sample data to make predictions or decisions without being explicitly programmed to do so. 




> [!question]
> 5.) What are applications of ML? (Unit 2 of AI Course).

> [!answer]-
> 1. Natural Language Processing
> 2. Image Processing
> 3. Facial Identification
> 4. Financial Modeling
> 5. Sentiment Analysis
> 6. Trajectory Prediction
> 7. Semantic Segmentation

> [!failure]




> [!question]
> 6.) What are the 4 paradigms of ML?

> [!answer]-
> 8. Supervised Learning.
> 9. Unsupervised Learning.
> 10. Semi-Supervised Learning.
> 11. Reinforcement Learning.

> [!success]



> [!question]
> What is Supervised Learning (short)?

> [!answer]-
> Supervised learning denotes the learning tasks when data inputs and corresponding target outputs are provided. The approach includes both classification and regression approaches. 



> [!question]
> What is Unsupervised Learning (short)?

> [!answer]-
> Unsupervised learning is concerned with discovering the hidden patterns in the data inputs and includes clustering as an important sub-domain. 



> [!question]
> Why would Unsupervised learning be considered an important frontier of machine learning?

> [!answer]-
> Because most big datasets do not come with labels; that is, the outputs are not known. 



> [!question]
> What is Semi-Supervised Learning (short)?

> [!answer]-
> This covers problems where only partial label information exists and combines Supervised with Unsupervised. 
> These methods are especially relevant when obtaining sufficient amounts of labeled data is prohibitively difficult of expensive, but large amounts of unlabeled data are relatively easy to acquire. 



> [!question]
> What is Reinforcement Learning (short)?

> [!answer]-
> Reinforcement learning denotes the learning setup where the goal is to find an action policy that achieves a given goal. 
> The model learns how to achieve that goal by trial-and-error interactions with its environment. 



## 1.1. Classification & Regression


> [!question]
> 7.) What is a training dataset?

> [!answer]-
> A dataset used by machine learning models to build its predictive mathematical functions.



> [!question]
> 8.) What is a Testing dataset?

> [!answer]-
> A dataset used to measure the performance of the developed ML model.



> [!question]
> 9.) What is a confusion matrix?

> [!answer]-
> A matrix to measure outputs where the:
> - Actual values are on the Y-Axis (rows);
> - Model Outputs are along the X-Axis (columns);
> Shows how many instances are correctly classified by the developed model. 


> [!question]
> What is Accuracy

> [!answer]
> Formula

$$
\mathbf{Accuracy} = \frac{TP+TN}{TP+FP+TN+FN}
$$


> [!question]
> What is Precision

> [!answer]
> Precision - think it's the P's.
> It's the total guesses of Positive values. If most predictions are correct, this will be close to 100%. 

$$
\mathbf{Precision} = \frac{TP}{TP+FP}
$$


> [!question]
> What is Recall

> [!answer]
> A False Negative means it should have been positive. This implies we are measuring correctness. 

$$
\mathbf{Recall} = \frac{TP}{TP+FN}
$$



> [!question]
> What is F-Score

> [!answer]
> A weighted average or Precision and Recall

$$
\text{F-Score} = \frac{2( \text{Precision} \cdot \text{Recall})}{( \text{Precision} + \text{Recall})}
$$



> [!question]
> 10.) How do you determine the best ML approach/solution for a problem?

> [!answer]
> Typically the technique that returns the highest evaluation performance is selected. 
> This relies on experience of the data scientists along with proper testing and evaluation of different approaches to best solve a given problem. 


> [!question]
11.) What is the trade-off between goodness of fit and complexity of the model?

> [!answer]
> It is a challenge to develop a ML model with many variables and free parameters. A model with too many degrees of freedom becomes complex and may always produce a good fit on its *training data*.
> On the other hand, if the model has insufficient degrees of freedom for the given task, there will be degrading influence on its produced fit. 



> [!question]
12.) How do you generally improve predicitive performance?

> [!hint]
> Page 20

> [!answer]-
> In general, when exposed to more observations, the model improves its predictive performance.



> [!question]
13.) What is overfitting? Why does it happen and how does it impact your model?

> [!answer]
> Overfitting is a scenario where the model performs very well on its training data but does not perform well on the testing dataset. 
> This happens when the model highly adapts to the training set.
> Overfitting will impact negatively on the degree of generalization on new data and should be avoided for solutions to be useful in practical applications. 



> [!question]
> What is Underfitting?

> [!answer]
> Underfitting happens when the model does not capture enough of the inherent structure in the training data.
> This results in poor performance with both training and testing sets.



## 1.2. Machine Learning Paradigms



> [!question]
14.) What does an efficient ML model do?

> [!answer]
> ?



> [!question]
15.) Give a brief explanation of the Supervised Learning paradigm. 

> [!answer]
> ?



> [!question]
16.) What is the objective of Supervised learning?

> [!answer]
> ?



> [!question]
17.) What happens to parameters of model during the learning process?

> [!answer]
> ?



They are updated until the optimum setting is achieved.

> [!question]
18.) What governs the parameter updating process during learning?

A specific loss function.
The objective becomes adjusting parameters to minimize the loss function. 

> [!question]
19.) What is typical loss function of regression?

The MSE.

> [!question]
20.) What is the typical loss function for classification problems?

Can be the number of wrongly classified instances. 

> [!question]
21.) What is the structure of the supervised learning procedure?

instances of training set are used to learn the model via classification/regression algorithm.
Then, modle is applied to predict the otupt for testing samples (not presented during model's training. 

> [!question]
22.) What type of Supervised learning would be applied to determine the current value of a home?

> [!question]
23.) Know Supervised learning techniques on page 22-23.

> [!question]
24.) What is unsupervised learning, when do we use?

The objective is to develop ML models to discover patterns and structures in training data. 

> [!question]
25.) What is "Dimensionality Reduction"?

the process of removing the irrelevant variables form the dataset. 

> [!question]
26.) What is an outlier?

> [!question]
27.) what are True and Fake outliers?

> [!question]
28.) What are Unsupervised Learning Techniques (page 25.)?


## 1.3. Reinforcement Learning

> [!question]
29.) What is Reinforcement Learning?

> [!question]
30.) What are the ingredients of Reinforcement Learning?

A.A.E.S.R.P.V.

> [!question]
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

54.) What is the issue with Centroid based clustering algorithms?

<details>
<summary>Click for Answer</summary>
They do not address fake outliers.
</details>

55.) Why is the above (Q: 54) an issue?

<details>
<summary>Click for Answer</summary>
Points get assigned to clusters even if they belong to no clusters.
</details>

56.) What does density-based cluster do?

<details>
<summary>Click for Answer</summary>
It identifies clusters by grouping dense data records together?
</details>

57.) What does density-based clustering allow the method to do (2 things)?

<details>
<summary>Click for Answer</summary>
1. It allows for arbitrarily shaped clusters; and 
2. allows the model to learn of outliers within the data.
</details>

58.) What concept is density-based clustering based on? 

> [!answer]- 
> It is based on the "$\varepsilon$-neighborhood" concept.


59.) What is the $\varepsilon$-neighborhood of a data record $P$?

> [!Answer]-
> It is the set of points contained in the shape of extension $2\varepsilon$, centered at $P$.

60.) How do we mathematically describe, in general, the $\varepsilon$-neighborhood of a point $P$ in a dataset $d$?

> [!Answer]-
> $$
N(P) = \left\{
q \in d | \mathbf{dist}(p,q) \le \epsilon
\right\}
> $$
> Where $N(P)$ is the number of data points.

61.) In the above, What does $N(P)$ indicate?

> [!Answer]-
> $N(P)$ indicates how dense the $\varepsilon$-neighborhood at $p$ is. 


# Unit 3. Regression

Q.) What is meant by Regression?

> [!Answer]-
> TODO

Q.) What are different types of regression analysis?

> [!Answer]-

Q.) How to use a simple linear regression model?

> [!Answer]-

Q.) What different metrics exist to evaluate regression models?

> [!Answer]-

Q.) What are logistic and quantile regression models?

> [!Answer]-

Q.) What are regularization approaches in regression analysis?

> [!Answer]-


## 3.1. Linear and Nonlinear Regression

> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 


## 3.2. Logistic Regression


> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 





## 3.3. Quantile Regression


> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 




## 3.4. Regularization in Regression Analysis



> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 




## 3.5. Regression Analysis in Python


> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 



# Unit 4. Support Vector Machines


> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 



## 4.1. Introduction to Support Vector Machines

> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 


## 4.2. SVM for Classification

> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 


## 4.3. SVM for Regression


> [!question]
> ?

> [!Answer]-



> [!question]
> ?

> [!Answer]-
> 



> [!question]
> ?

> [!Answer]-
> 


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

Q.) What does the information gain technique provide higher-ranking values to? Why?

> [!Answer]-
> It provides higher ranking values to the features having values that are more distinct. 
> It does this because, typically, the purity of the corresponding partitions is high. 

Q.) Are there any issues with how the information gain technique performs splitting? Explain.

> [!Answer]-
> Yes, using an identifier property as an example, all values in feature $f_I$ would be distinct. This implies that each corresponding partition contains a single instance of a single class. 
> The entropy of $Info_{f_I}(D_I)$ of such a feature $f_I$ is zero because the partition is completely homogenous. 
> Splitting the tree based on that feature does yield high information gain, using an ID-field for classification is a poor choice in terms of generalization ability of the resulting classifier. 

Q.) How doe C4.5 handle the problem that information gain appears to suffer from?

> [!Answer]-
> By normalizing the $gain(f)$ to form a new value $gainRatio(f)$.

Q.) Explain what the Gain Ratio is and how it is calculated

> [!Answer]-
> ...

$$
\begin{align}
\tag{5}
\mathbf{gainRatio}(f) &= \frac{\mathbf{gain}(f)}{\mathbf{SplitInfo}(f)}
\\
\tag{6}
\mathbf{SplitInfo}_f(D) &= -\sum_{i=1}^v{\left(
\frac{|d_i|}{|D|} \cdot \log{\left(\frac{|d_i|}{|D|}\right)}
\right)}
\end{align}
$$

The `SplitInfo` term is the normalizing factor that is inversely proportional to the ranking measure `gainRatio(f)`. Its calculation is based on the average sum of the ratio between the number of instances in a partition over the total number of instances. 

Note: SplitInfo is like `Gain` - the $P_k = |d_i| / |D|$.


Q.) Explain how the $\mathbf{SplitInfo}(f)$ value may lead to instability.

> [!Answer]-
> The value decreases as the number of instances in each partition decreases with respect to the total number of instances. 
>  The value may decrease to approach the zero value, which can lead to unstable ranking measure due to issue with divide by zero. 

Q.) What other advantages, besides the different handling of splitting, does the C4.5 algorithm have over the ID3 algorithm?

> [!Answer]-
> C4.5 can deal with both continuous and discrete features. 
> It handles missing values and applies tree pruning AFTER the process of the tree induction.

Q.) What features does the Gain Ratio technique provide high rank to?

> [!Answer]-
> It provides high rank to features that split the dataset into *unbalanced* partitions, such that one of the partitions is larger than the other. 

Q.) How does the CART decision tree classifier measure impurity?

> [!Answer]-
> The CART decision tree classifier uses a Gini index $Gini(D)$ to measure the impurity in a dataset of instances. 

Q.) For the CART decision tree classifier, how is rank of a feature measured?

> [!Answer]-
> Rank of any feature $f$ is measured by the amount of reduction in impurity.
> The feature that maximize the impurity reduction is selected as an important feature for the classification problem. 

Q.) Walk through the calculation for feature ranking following the Gini Index.

> [!Answer]-
> ...

Rank $\Delta \mathbf{Gini}(f)$ of a feature $f$ is calculated as the difference between the Gini index of the total dataset of instances and the Gini index of the datasets partitioned by the feature:

$$
\Delta \mathbf{Gini}(f) = \mathbf{Gini}(D) - \mathbf{Gini}_f(D)
$$

The value $\mathbf{Gini}(D)$ that represents the impurity in a dataset is calculated as:

$$
\mathbf{Gini}(D) = 1 = \sum_{k=1}^m{\left(
P_k^2
\right)}
$$

Where $P_k$ is the probability that an instance in a dataset $D$ belongs to class $k$ in the $m$ classes of $D$. 

Q.) Why kind of split does the Gini Impurity index consider? 

> [!Answer]-
> It considers only a binary split for a feature $f$ in $D$. 

Q.) Which feature is selected for splitting following the CART...?

> [!Answer]-
> The selected splitting point is a value in the feature vector $f$ that is **best** at splitting the instance in $D$ into two partitions $d_1$ and $d_2$ only. 

Q.) How do we calculate $\mathbf{Gini}_f(D)$?

> [!Answer]-
> ...

The value is calculated as the weighted sum of the impurity in each of the two sets $d_1$ and $d_2$ that the dataset is split into:

$$
\mathbf{Gini}_f(D) = \frac{d_1}{D} \mathbf{Gini}(d_1) + \frac{d_2}{D} \mathbf{Gini}(d_2)
$$

Q.) Walking through the example on page 115 of the course book, calculate the information gained by partitioning the dataset according to the feature "age". 

> [!Answer]-
> TODO
> We want to classify if the person will purchase a computer. This is classification, so it is labeled data. 
> First What is the Entropy for purchasing a computer? 
> Then, what is the Entropy purchasing a computer AND the persons age? 
> HINT: the latter will be the sum of ages
> the information gained is the decrease in entropy. 

## 5.3. Decision Tree for Regression

Q.) What is **regression**?

> [!Answer]-
> A method of predicting the numerical value of a target variable given one or more independent variables. 

Q.) How can we perform regression with a decision tree?

> [!Answer]-
> We can construct a tree with ID3 algorithm that uses the standard deviation reduction method instead of the information gain method. 

Q.) What is standard deviation?

> [!Answer]-
> A measure of the degree of variation in a set of numerical values. 

Q.) Is a feature vector of similar values homogeneous or heterogeneous?

> [!Answer]-
> Homogeneous. 


Q.) What is the standard deviation of a completely homoneneous feature vector?

> [!Answer]-
> Zero.

Q.) What is the class, or target varialbe, in a decision tree regression problem?

> [!Answer]-
> It is a vector of numerical values instead of categorical ones. 

Q.) What is the mean and standard deviation for decision tree regression? 

> [!Answer]-
> ...

$$
\begin{align}
\mu_c \approx \bar{c} &= \frac{\sum_{i=1}^n{(c_i)}}{n}
\\
\sigma_c \approx S_c &= \sqrt{
\frac{\sum_{i=1}^n{(c_i - \bar{c})^2}}{n}
}
\end{align}
$$

Q.) How do we calculate the standard deviation of the target vector partitioned based on the feature vector $x$?

> [!Answer]-
> ...

Let $P(v)$ be the probability of $v$ occurring in the target vector $c$. Its value is equal to the ratio of the number of instances whose value is $v$ to the total number of instances. 

$$
S(c,x) = \sum_{v \in x}{\left( P(v) \cdot S_c(v) \right)}
$$


Q.) What is the reduction in standard deviation?

> [!Answer]-
> TODO

Reduction in Standard Deviation:

$$
SDR(c,x) = S(c) - S(c,x)
$$

This is measured for each feature and the feature with the largest value is considered to be most important. 

Q.) What is the Coefficient of Variation? 

> [!Answer]-
> TODO

It is considered a "Percentage Ratio" of the standard deviation to the mean value of a feature vector. It is used to STOP branching in the decision tree induction process. 

Calculated as:

$$
CV = S / \bar{x} \cdot 100\%
$$

## 5.4. Decision Tree Construction


Q.) How have the decision trees so far (ID3, C4.5, and CART) been constructed?

> [!Answer]-
> The have been constructed in a **greedy**, top-down manner.

Q.) Walk through the algorithm to build a Decision Tree.

> [!Answer]-
> The algorithm pertaining to *these* approaches uses a recursive function to iterate over the set features:
> 1.) Algorithm selects the highest ranked feature (greedy) from the feature set.
> 2.) A root-node is created to represent this feature. The feature is also removed from the list of features to consider in the next iteration.
> 3.) Branches are created down for this parent node (top-down), with each branch labeled by a distinct value (or range of values) for the corresponding feature value. 
> 4.) If the instances in the input dataset that have this specific feature value are of different class labels, then the next highly ranked feature is to be added as a child decision node from this branch. Else; if all the instances of this feature value are the same class $C$, then the child node from this branch is a leaf node that is labeled by this class $C$. 
> 5.) This process continue recursively until all terminal nodes of the tree are leaf nodes.

Q.) Define what are "decision nodes" and what a "leaf nodes".

> [!Answer]-
> A decision node is a node that represents a feature that may branch depending on the features values. 
> A leaf node is a node that represents a class label. 

> below question and function (p. 119) probably needs more study

Q.) Describe the function `BuildTree()`

> [!Answer]-
> ...

```python
def BuildTree(D: DataSet, A: Set[Attribute]) -> DecisionTree:
	N: Node = create_node()
	# get Info(D)
	# if Info(D) == 0; return N as leaf node w/class C_D
	# if len(A) (|A|) == 0; return N as leaf w/class C_m for majority of instance in D
	# 
```

Q.) Can the ID3 algorithm operate on continuous values?

> [!Answer]-
> No, but a discretization process can be applied to features of continues values in the pre-processing step. 

The rest of the section explains an example.

## 5.5. Decision Tree Pruning

Q.) What is generally the relationship between the complexity of the constructed tree and the size and heterogeneity of the input data. 

> [!Answer]-
> Complexity increases as the size and heterogeneity of the input dataset also increases.
> Particularly valid when the dataset contains largescale, real-life data that may contain noise and outliers. 

Q.) Is it easy to interpret any decision tree?

> [!Answer]-
> No, it becomes difficult to interpret decision trees with numerous decision rules. 

Q.) What issue can too much complexity cause?

> [!Answer]-
> It can lead to overfitting the training data. It happens when rules fit the limited dataset of training instances perfectly and fail to reliably classify new instance exemplars. 

Q.) How can we handle the overfitting problem?

> [!Answer]-
> One answer is Tree Pruning. 

Q.) How does tree pruning work (high-level - short answer)?

> [!Answer]-
> It decreases the size of the tree to make it less complex. 

Q.) What can happen if we prune too many branches?

> [!Answer]-
> Over pruning the tree can lead to underfitting, where the pruned tree becomes very small and too trivial to sufficiently classify instances. 

Q.) What two flavours does the tree pruning technique come in?

> [!Answer]-
> You have Pre-Pruning and Post-Pruning.

Q.) Please explain what Pre-Pruning is and how it works. 

> [!Answer]-
> Pre-pruning is a process that *avoids* building up the low-discriminating sections while the decision tree is being constructed. 
> When a specific condition is met, the constructing algorithm avoids adding a new decision node to split the instances among the resulting branches. 
> Instead, it adds a leaf node with the label of the **most frequent** class among the pretraining instances. 

Q.) What is the dependency of the concrete form of the pruning condition?

> [!Answer]-
> It is dependent on the **feature-ranking** measure used in the decision tree induction.

Q.) What is the halting condition for building a branch in pre-pruning?

> [!Answer]-
> If the used ranking measure is below a pre-specified threshold, then further partitioning is halted. 

Q.) What is a method of Top-Down Pruning?

> [!Answer]-
> Pessimistic error pruning (PEP).

Q.) Please Explain what Post-Pruning is and how it works.

> [!Answer]-
> Post-pruning is a process that removes spurious sub-trees from the fully constructed decision tree and replaces them with a leaf node with the label of the most frequent class among this sub-tree. 
> How? It measures cost complexity of the tree for each decision node in a bottom-up manner. 
> If this cost complexity of the tree increases by replacing a decision node with a leaf node, then the descendent sub-tree of this decision node is pruned.

Q.) Which of our learned approaches implements Post-Pruning?

> [!Answer]-
> The CART approach implements post-pruning.

Q.) What is cost complexity?

> [!Answer]-
> A function of the number of leaves and the rate of error (misclassified instances) in the tree. 

$$
R_{\alpha}(T) = R(T) + \alpha |T|
$$

- $R(T) =$ total training error of leaf nodes.
- $|T| =$ the number of leaf nodes.
- $\alpha =$ complexity parameter (a whole number).

https://www.geeksforgeeks.org/machine-learning/how-to-choose-a-in-cost-complexity-pruning/

You pick the alpha, higher values lead to simpler trees. 

Q.) What methods are Bottom-Up Pruning?

> [!Answer]-
> Reduced Error Pruning (REP),
> Minimum Cost Complexity Pruning (MCCP),
> Minimum Error Pruning (MEP).
> https://en.wikipedia.org/wiki/Decision_tree_pruning

## 5.6. Decision Trees in Ensemble Methods

Q.) What is an **Ensemble method** in simple terms?

> [!Answer]-
> It is a meta-method that combines a series of machine learning algorithms to improve learning performance. 

Q.) ?

> [!Answer]-
> The learning algorithms are used as base learners that are often weak learners. 

Q.) What is a "weak learner"?

> [!Answer]-
> A weak learner is a poor learning algorithm that performs slightly better than a random classifier. 

Q.) What is the error rate of a weak learner for binary classification problems?

> [!Answer]-
> It should be close to but less than 50%.

Q.) Can a decision tree be used as a weak learner? Why?

> [!Answer]-
> Yes it can, by controlling its maximum depth we can produce weak classifiers.

Q.) What is a "shallow" decision tree?

> [!Answer]-
> A decision tree that is significantly pruned to only have a few branches.

Q.) What is a decision "stump"? 

> [!Answer]-
> A simple decision tree of one-level.
> It finds a threshold for which a single feature can be partitioned into two parts around it. 

Q.) What is the main principle around ensemble methods?

> [!Answer]-
> Instead of training a single strong classifier on the whole input space, it is better to train many weak base-classifiers that are good at different parts of the input space. 

Q.) What are the two sets of aggregated base classifiers of Ensemble Methods?

> [!Answer]-
> They are either:
> a single learning algorithm like a decision trees (homogenous weak learners);
> or different learning algorithms (heterogeneous weak learners).

Makes sense when you spell it out.

Q.) What are two prominent types of ensemble methods of homogenous weak learners?

> [!Answer]-
> The bagging method.
> The boosting method.

Q.) Give at least one example of a heterogeneous weak learner.

> [!Answer]-
> The stacking method.

#here page 123 bottom paragraph.

Q.) What is first type of ensemble method for homogenous weak learners?

> [!Answer]-
> The Bagging, or Bootstrap Aggregation, ensemble method. 
> **B**ootstrap **Agg**regation.

https://towardsdatascience.com/tree-ensembles-theory-and-practice-1cf9eb27781/
> [!hint]-
> > [!example] 
> > You basically randomly sample a small set from total;
> > Then you build a small decision tree.
> > And they vote.

Q.) What is "Bootstraping"?

> [!Answer]-
> Refers to a method of generating bootstrap samples.
> Bootstrap samples are samples that are subsets of a specific number of instances $x$ that is less than the total number of instances $|X|$. 
> The generating process begins with an initial subset of $x$ instances. 
> Each of those $n$ subsets is used to form a decision tree that is controlled to be a decision stump, or simple shallow-depth decision tree. 
> Then, the bagging method is trained to build $n$ weak learners. 

> [!Question]
> What are the steps of Bootstraping Aggregation? 

> [!Answer]-
> ???

Q.) What is the contribution of each learner considered in the Bagging method?

> [!Answer]-
> Each method is considered a "vote" to one of the class labels of the problem. 

Q.) If the Bagging method has many weak learners, how is a final decision made?

> [!Answer]-
> A majority vote is determined by calculating the average (mean) voted class labels. 

Q.) How are weights distributed to votes in Bagging method? Why are these weights assigned?

> [!Answer]-
> The aggregation step provides an equal weight to each vote; which yields an unweighted average. 
> They are assigned because homogenous weak learners are formed independently and in parallel. 


Q.) What is the Aggregation step in the bagging method?

> [!Answer]-
> Where votes are counted. 

Q.) What is another example of an ensemble method for homogenous weak learners? 

> [!Answer]-
> Random Forest method is another example of an ensemble method for homogenous weak learners. 

Q.) How is Random Forest method done?

> [!Answer]-
> It follows the bootstrapping method with an update to the bootstrapping step.
> After generating $n$ samples, the instances in each sample have a random subset of $m$ features rather than the original set of features $M$. 
> This means the random forest generates $n$ samples of $m$ features. 

Q.) How many advantages does the Random Forest have over bootstrapping and what are they? 

> [!Answer]-
> It has two main advantages:
> 1.) It enables the forest to efficiently handle a high number of features (dimensionality) in a problem. 
> 2.) It reduces the correlation between the predicted class label from highly different learners. 

> [!question] 
> What is the Boosting Method?

> [!Answer]-
> The performance of the homogeneous weak learners is updated by the training samples, iteratively. 
> It is based on the Bagging method, but it applies a sequential fitting of the formed learners in an iterative manner. 

> [!question] 
> Provide steps to creating a model following the Boosting Method.

> [!Answer]-
> Do a Bagging model
> - Get $n$ samples from $N$.
> - Make decision tree.
> Each instance is provided with an initial weight of $1 \over k$; where $k$ is the number of class labels in the dataset. 
> However, that is only true on the initial selection. In the next iteration, the weight of misclassified instances is updated by increasing its value. Instances of higher weight have a higher probability of being selected in the samples.
> This continues until a stopping condition - like performance of the model is no longer increasing.

> [!question] 
> Q.) How should performance behave after each iteration of Boosting Model training?

> [!hint]-
> Super intuitive.

> [!Answer]-
> The performance of the model should **increase** at each iteration where the learners of the model are fitting more instances correctly. 

> [!question] 
> What is the stopping condition of the Boosting method dependent on?

> [!Answer]-
> It depends on the **domain problem**!
> > [!example]
> > It is sufficient to have some maximum accuracy threshold.

> [!question] 
> Are there any risks associated with using a Boosting method? What are they, if they exist?

> [!Answer]-
> Yes, there is an increased risk of overfitting because of the focus on misclassified instances that may be outliers or noise!

> [!question]
> What was the first Boosting algorithm to take advantage of weak learners?

> [!info]-
> [Boosting and Gradient Boosting](https://towardsdatascience.com/tree-ensembles-theory-and-practice-1cf9eb27781/)

> [!Answer]-
> The "Adaptive Boosting", or Adaboost.

Q.) How does Adaboost Algorithm work?

> [!Answer]-
> Assigns the higher weight to misclassified instances so that these instances receive the high probability for classification in the next iteration. 
> It also assigns the higher weight to the learners that shows a higher classification accuracy. 
> Two sets of weights. 
> Therefore, the vote of the learner of higher accuracy receives a higher weight in calculating the average vote. 
> The final vote in the Adaboost method is a weighted average of the votes of the learners. 
> Iterative model continues until a stopping condition is met. 

Q.) What is Gradient Boosting?

> [!Answer]-
> This is an Adaboost method that weighs based on a loss function. 
> The loss function of each of the learners is the opposite of the gradient descent of the current fitting error. 

Q.) What is the Extreme Gradient Boosting method?

> [!Answer]-
> Also known as XGBoost; the loss function of this method computes the second order gradient to provide more information to classifier and reach higher accuracy. 

# Unit 6. Genetic Algorithms

> [!info]
> What to learn:
> - The motivation for genetic algorithms.
> - The definition of a genetic algorithm.
> - The different phases of genetic algorithms.
> - The applications of a genetic algorithm to solve the knapsack problem.
> - The implementation of genetic algorithms in Python. 

> [!question]
> When are the earliest forms of life understood to have began existing on this planet?

> [!Answer]-
> over 3.5 Billion years ago. 

> [!question]
> What is a "Population"? 

> [!Answer]-
> For use in machine learning, a population is simply a group of objects in a particular space. 

> [!question]
> What is the "driving force" behind variations across individuals of a population?

> [!Answer]-
> Genetic evolution by natural selection.

> [!question]
> Is evolution in nature a continuous process? Why?

> [!Answer]-
> Yes, it is a continuous process because the environment is constantly changing, so organisms are constantly adapting to their changing environment. 

> [!question]
> What is the "Theory of Evolution"?

> [!Answer]-
> Darwin's theory of evolution is a hallmark of biological change across time that explains natural biological changes in and across species as adaptations to the species' habitat and environment. 

> [!question]
> Is the environment of evolution, as an optimization technique, continuously changing?

> [!Answer]-
> No, the environment is considered static. 

> [!question]
> Evolution as optimization, when does the process of evolutionary adaptation end?

> [!Answer]-
> It continues until the fitness of individuals cannot be improved further, in their static environment, which stops the evolution process. 

> [!question]
> Based on when evolutionary optimization stops, what can we say about the last generation of individuals?

> [!Answer]-
> We can confidently state that an individual in the last generation is considered optimal and no individual can be better.

> [!question]
> High-level, how does an evolutionary algorithm work?

> [!hint]
> Looking for 2 parts.

> [!Answer]-
> An evolutionary algorithm initially generates a set of solutions to a problem in a random way, and tests each of these solutions through a fitness function. 
> 1.) Generates set of solutions in a **random** way.
> 2.) Tests each solution through a fitness function.


> [!question]
> How are the best solutions of one solution set translated into the next solution set?

> [!Answer]-
> The best possible solutions are **evolved** to the next generation in the evolution process. 



> [!question]
> How long does this process of evolution continue on for? Or better, how do we know when the process should come to an end?

> [!Answer]-
> The process continues until a near optimal solution is obtained, and the output of the fitness function does not change. 



> [!question]
> How can you define evolutionary algorithms?

> [!Answer]-
> Evolutionary algorithms constitute a generic metaheuristic model for optimization problems that operates on a population-based representation of the solution space. 



> [!question]
> Define again, what is a population of an evolutionary algorithm?

> [!hint]
> Last time we defined it more generally for Machine Learning. This is tailored for Evolutionary Algorithms.

> [!Answer]-
> It is a set of feasible solutions that may contain the best solution for a specific problem. 



> [!question]
> What does the Evolutionary Algorithm technique involve?

> [!Answer]-
> The technique involves:
> 1. The transformation of a population from one generation to the next where properties of individuals are represented by a code that can be modified to yield new exemplars. 
> 2. It uses and adapts the concept of biological DNA sequences, or genes, where a child shares many characteristics of the two DNA sequences of their parents. 
> 3. Individuals that show a high amount of fit to the optimization objective are allowed to breed the next generation.



> [!question]
> What is a "Gene"?

> [!Answer]-
> It is a heredity unit that is transferred from a parent to their offspring, or gene, holds some characteristic of the offspring.



> [!question]
> What kind of technique is an evolutionary algorithm?

> [!Answer]-
> It is a heuristic technique.



> [!question]
> What is a Heuristic Technique?

> [!Answer]-
> It is a practical problem-solving approach that relies on intuitive rules of thumb or shortcuts rather than exhaustive mathematical methods to reach a solution. 
> Think of it like guess-and-check.



> [!question]
> What is a pro and a con of using heuristic techniques?

> [!Answer]-
> A benefit can be speed and simplicity. However, a con would be that the technique cannot guarantee the global optimility of the resulting solution, that you have the best answer. 
> The achieved solutions commonly prove to be sufficient for many practical purposes. You get very good answers within a reasonable timeframe. 



> [!question]
> Evolutionary algorithms are a broad class. What are 3 subclasses?

> [!Answer]-
> 1. Genetic algorithms; which mock the biological genetic evolution process.
> 2. Swarm algorithms; which simulate the movement of a group of animals towards a specific target, like fish or birds.
> 3. Ant Colony algorithms; which simulate the communication between insects to find the shortest path between their nest and a food source. The indirect communication mechanism is called "stigmergy". 



> [!question]
> What kind of optimization method is a genetic algorithm?

> [!Answer]-
> It is a heuristic optimization method. 


> [!question]
> What are some possible applications of Genetic Algorithms in machine learning?

> [!Answer]-
> 1. Feature Selection - features used in ML application are evolved in order to find the subset that provides the best overall model performance. 
> 2. Hyperparameter tuning - ...
> 3. Optimization of structures and learning rules for artificial neural networks.



> [!question]
> What are **hyperparameters**?

> [!Answer]-
> A hyperparameter is a variable that influences a model's behaviour and output but is not adjusted by the training process. 
> > [!example] 
> > - The number of clusters in k-means algorithm;
> > - The limits on the depth of trees in decision tree learning.


## 6.1. Genetic Algorithm Definition

> [!question]
> What are Genetic Algorithms?

> [!Answer]-
> They are a class of evolutionary algorithms that is inspired by the biological genetic evolution of living organisms (Sammut, 2011).



> [!question]
> What is the purpose of using a Genetic Algorithm?

> [!Answer]-
> The algorithm is used to simulate the reproduction of individuals in a population in order to solve a specific optimization problem. 
> The simulated evolution aims at iteratively exploring the space of possible solutions to find the optimum, or near-optimum, solution to the given problem. 



> [!question]
> What is **DNA**?

> [!Answer]-
> DNA stands for Deoxyribonucleic Acid and is a self-replicating material that is present in all living organisms, functioning as a carrier of genetic information. 



> [!question]
> What are individuals of a biological population made up of?

> [!Answer]-
> Cells.



> [!question]
> What are the constituent parts of individuals encoded with? 

> [!Answer]-
> Cells are encoded by a set of entities known as genes, or DNA. 



> [!question]
> For yourself, briefly explain the difference between a gene and DNA please. 

> [!Answer]-
> DNA can be thought of as the entire library. It is the chemical substance that makes up your chromosomes. It is the raw material holding all the instructions.
> DNA is a double helix made of nucleotides (A, C, G, T).
> A Gene is a specific recipe inside one of the books. It is a specific segment of DNA that codes for a specific protein or function. 
> A Gene is a functional unit within a DNA strand, a specific sequence of bases that has a purpose. 
> Not all DNA is a gene. 



> [!question]
> What is the difference between DNA and Chromosomes?

> [!Answer]-
> DNA is purely chemical information. It is a polymer chain made of nucleotides (Adenine, Guanine, Cytosine, and Thymine). Can be thought of as a raw string of letters. DNA exists all the time, but usually in loose, uncoiled state called **chromatin**. 
> A Chromosome is a structure, it is DNA wound tightly around proteins called **histones**! It is DNA plus scaffolding to fit inside the cell nucleus. A Chromosome appears when the cell prepares to divide. The chromatin tightens up into compact, distinct rods. 
> Again, DNA is the material. A Chromosome is the container and structure holding the material in a cell. 



> [!question]
> How many pairs of chromosomes does every human cell contain?

> [!Answer]-
> 23.



> [!question]
> If we translate biology to computer science, and a chromosome as a series of bits, what is the value of each bit called?

> [!Answer]-
> We would call it a **genotype**.
> It it were an array, I think each element would be a **gene** and the actual value is the "Genotype". 



> [!question]
> In Darwin's theory of natural selection, how is the opportunity for survival for highly fit individuals? In accordance with the principle of the survival of the fittest, is the opportunity large or small?

> [!Answer]-
> Large



> [!question]
> How does the biological evolution process describe genetic changes in a population?

> [!Answer]-
> The genetic changes in a population are described through successive generations. That is, the genetic changes are the variations that occur in the reproduction process on the genetic level. So, they are therefore inherited by the next generations. 



> [!question]
> In what two important ways do genetic changes occur in genetic algorithms?

> [!Answer]-
> Crossover and mutations of the genetic structure. 


## 6.2. Genetic Algorithm Phases

> [!question]
> How many phases does the general outline of a generic algorithm consist of?

> [!Answer]-
> 5 phases.



> [!question]
> What are the 5 phases of a genetic algorithm?

> [!Answer]-
> 1. Creation of initial population.
> 2. Evaluation of the fitness function.
> 3. Selection of the fittest.
> 4. Crossover.
> 5. Mutation of the genetic Structure.



> [!question]
> What happens at the end of the 5 phases?

> [!hint]
> What new thing do we have?

> [!Answer]-
> A new population is produced based on the current population!



> [!question]
> Do you run through a genetic algorithm once?

> [!Answer]-
> No! A genetic algorithm goes through multiple iterations. 



> [!question]
> What is the basis of each iteration of a genetic algorithm?

> [!Answer]-
> Each iteration is formed by the previously mentioned five phases.



> [!question]
> When do the iterations stop?

> [!Answer]-
> The iteration stops when an acceptable level of fitness is achieved by at least one individual. 
> That is, when no further improvement in fitness can be achieved, or when a pre-defined maximum number of iterations has been reached. 
> 



> [!question]
> How might be otherwise interpret the iterating process in the genetic algorithm?

> [!Answer]-
> It can be interpreted as a searching process that aims at finding successively better solutions. 



> [!question]
> What are the 5 phases of the genetic algorithm? Please explain briefly what each phase is responsible for.

> [!hint]
> - What goes in?
> - What comes out?
> - What process maps inputs and outputs?

> [!Answer]
> - 1.) Initialization Phase:
> > - Data comes in.
> > - Individuals of the population are generated randomly in such a way that the corresponding chromosomes have a high coverage of the solution domain. 
> > - The number of genes in individuals' chromosomes is dependent on the problem.
> > - Output is the initial population.
> - 2.) Evaluation Phase
> > - Population comes in.
> > - Each individual is measured by a fitness function. 
> > - The input to the function is the chromosome of the individual.
> > - The output of the function is the fitness score of the individual. 
> > - The output of the phase is the Evaluated population. If in the last iteration, then the output is the best solution found so far.
> - 3.) Selection Phase
> > - The Evaluated population come in to this phase.
> > - Individuals with the highest fitness scores are selected for generating the new population. 
> > - Fitness scores typically must exceed a specific threshold to be selected, where the threshold constitutes a parameter that is defined according to the problem. 
> > - This phase ensures the newly generated population has better fitness than the current population.
> > - The Output are Candidates to reproduce for the next generation.
> - 4.) Crossover Phase
> > - Inputs are the parents from the current generation that met criteria from the selection phase. 
> > - Output are offspring of the parents.
> > - The process mixes the genes from parents' pair of chromosomes. This is the Crossover process, where some random point(s) (i.e. the crossover point(s)) have to be determined in the chromosomes of the parents. 
> > - Then, gene threads are cut and exchanged around the crossover point to create new threads. 
> - 5.) Mutation Phase
> > - Inputs are the offspring from the Crossover phase. 
> > - Outputs are the population of the next generation.
> > - The process is randomly flipping genes at arbitrary locations in the individual chromosome. 



> [!question]
> What is a "Fitness Function"?

> [!Answer]-
> A **Fitness Function** is used as an objective function that summarizes how well the designed solution is achieving a set of aims to measure how well a chromosome performs in an environment. 



> [!question]
> How does Crossover work?

> [!Answer]-
> The process requires a crossover point, or points, to be determined in the chromosomes of the parents. Then, gene threads are cut and exchanged around the crossover point to create new threads. 



> [!question]
> What types of crossover methods exist?

> [!Answer]-
> There are single-point and multi-point crossover methods. 
> In Single-point: locus is randomly chosen to exchange subsequences around. 
> In Multi-point: A set of points is chosen at random and corresponding sections are swapped. 



> [!question]
> What is a **Locus**?

> [!Answer]-
> It is a specific point in the chromosome. 
> I think it is arbitrary, you just call the point a "locus".



> [!question]
> What is a **Mutation**?

> [!Answer]-
> In genetic algorithms, a mutation is a change that genes can undergo in their structure caused by the deletion, insertion, or rearrangement of the chemical code of which they are composed. 



> [!question]
> What is the purpose of the Mutation Phase?

> [!Answer]-
> The main objective is to prevent a population from falling into local optimum solutions too quickly. 



> [!question]
> What is the "Genetic Algorithm Structure"?

> [!Answer]-
> The overall outline of the basic genetic algorithm can be described in the following steps:
> - 1.) Initialization Phase - algorithm generates a random population of $n$ chromosomes. The population represents the initial set of solutions and each chromosome in the population represents a possible solution for the domain problem.
> - 2.) Repeat the following steps until convergence:
> 	- Fitness: evaluate the fitness $f(S)$ of each chromosome $S$ in the current population.
> 	- Selection: Select the chromosome having the highest fitness score from the population. Each pair of selected chromosomes are mated together to create the new offspring.
> 	- Crossover: Apply crossover between the parents to form a new offspring (child) that shares some of the characteristics of both parents.
> 	- Mutation: Mutate the new offspring at some positions in the chromosome.
> 	- Replace: Replace the current generation by the new generation.
> - 3.) Return the final population.

## 6.3. Genetic Algorithm Example: Knapsack Problem


> [!question]
> What is the Knapsack problem?

> [!Answer]-
> It is a famous problem in Combinatorial optimization. It can be stated as follows:
> - Given a set of items, each item has a weight and a value.
> - Given a knapsack of a maximum capacity, considered as the overall weight that the knapsack is limited to hold.
> - The problem is to select a subset of items so that:
> 	- The total value is as large as possible; and
> 	- the total weight is less than or equal to the limit.
> You are basically going to pawn off some goods. 



> [!question]
> How do you formulate the Knapsack problem?

> [!Answer]-
> The problem is to select the subset of items from a set of $N$ items. 
> Each item $x_j$ in $n$ items has a profit $p_j$ and weight $w_j$. 
> The requirements of the selected subset of items is that the total profit of these items is **maximized**. 
> The constraint is that the total weight of the items does not exceed a specific capacity $M$. 



> [!question]
> What is the solution set for a Knapsack problem?

> [!Answer]-
> It is a subset of items $x_j$ which represents a solution $S$ for the problem. 



> [!question]
> What is the target in terms of a fitness function?

> [!Answer]
> ...

The target is to maximize the value of the fitness function:

$$
\tag{1}
f(S) = \sum_{j=1}^n{\left( p_j \cdot x_j \right)}
$$
Subject to the constraint that the maximum allowed capacity is not exceeded. 

Where:
- $f(S) =$ fitness function that evaluates the solution.
- $x_j =$ a binary variable that indicates 1 if item is selected and 0 if not. 


> [!question]
> What does the solution (chromosome) $S$ look like in this problem?

> [!Answer]-
> $S$ is considered as a list of $n$ bits and $j$ is its position in the list. So, `S = [0110101]` is a possible solution. 



> [!question]
> Since the number of solutions in the evolutionary algorithm is $m$, what is the feasibility of each solution?

> [!Answer]-
> ...

It is tested following the constraint:

$$
= \sum_{j=1}^n{\left( x_j x_j \right)} \le M
$$



> [!question]
> Do we allow infeasible solutions, that break constraints, in the evolution steps?

> [!Answer]-
> Yes we do.



> [!question]
> If a solution breaks the constraint and is allowed to exist, is there any special handling of that individual?

> [!Answer]-
> Yes, a penalty is imposed to the fitness of that solution. 



> [!question]
> Please describe how a penalty is determine in a genetic algorithm.

> [!Answer]-
> The penalty that is imposed is proportional to the total amount of excess in the knapsack as follows:

$$
\tag{2}
\mathbf{Penalty} = Q \cdot t(M - \sum_{j=1}^n{\left( w_j \cdot x_j \right)})
$$
Where:
- $Q =$ considered a sufficiently large and positive number. 
- The function ...

$$
t(z) =
\begin{cases}
0 &\text{if} & z \ge 0
\\
-z &\text{if} & z \lt 0
\end{cases}
$$

So fitness function adjusted according to the penalty as:

$$
\tag{3}
f(S) = \sum_{j=1}^n{\left( p_j \cdot x_j \right)} -
 Q \cdot t(M - \sum_{j=1}^n{\left( w_j \cdot x_j \right)})
$$

> [!quote]
> Page 135 does a Knapsack solve


## 6.4. Genetic Algorithm in Python

> [!danger]
> Skipping because Python Specific implementation not on exam

> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



> [!question]
> 

> [!Answer]-
> 



---
