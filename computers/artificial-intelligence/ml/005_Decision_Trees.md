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

# 5. Decision Trees

pp. 107-126

On completion of this unit, you will have learned:
- what a decision tree is and how it is used in supervised learning.
- the different  approaches to construct a decision tree.
- the purpose and the types of feature-ranking techniques used in decision trees.
- what is meant by tree pruning and whether it occurs before or after  the tree construction.
- how a decision tree classifier helps in building up an ensemble model.

## Introduction

**Decision Trees** represent a group of classification techniques that are based on the construction of a tree like structure. As the name suggests, it hosts a structure that represents a set of nested decisions. These decisions make use of the provided feature information in a sequential manner to *categorize* the input object. 

These are used if fields such as:
- image processing.
- character recognition.

Additionally, other areas implementing decision trees include:
- medicine
- financial analysis
- astronomy
- manufacturing
- production
- molecular biology.

## 5.1 - Introduction to Decision Trees

**Decision Trees** are classifiers. They belong to the field of *supervised learning*. 

Building the decision tree structure and using it for classification of new samples is a two-step process:
- Learning Step:
	- induction of a tree structure based on the training data of labeled data instances.
- Decision Step:
	- Includes classification of testing data on non-labeled instances. 

Each instance is characterized by a set of features. Labeled instances in the training set are those of a known class label. 

Structure of decision tree includes decision nodes, branches, and leaves. Each internal node in the tree represents a decision based on a feature. 

The branch from this node is selected based on the value of this feature. 

Each tree branch represents a conditional statement. And the root node represents the most important feature of the data objects with respect to the classification problem at hand. 

We now look at an example in the course book. 

Consider a dataset of three instances. There are only two class labels, $C_1$ and $C_2$. For simplicity, each instance is characterized by only one feature $f_1$. 

Ok, so Given a set of features, it is like, if we have this feature, go right, else go left. Then at the next leaf do the same until you reach your class. 

Now, given the dataset contains more than one feature, then the decision tree classifier uses a ranking technique to detect their degree of importance to the given classification problem.

The most important feature is the root node, and we descend from there. I suppose as we make decisions, we test different features and as such, we might not test all features as some are not relevant in certain classifications. 

A **decision rule** is a group of conditions that enable the classifier to determine the class membership of an instance.

Any path from the root node of the tree to a leaf node represents a decision or classification rule. 

The decision tree helps visualize a set of decision rules. So far we have made it sound simple but more features can explode with complex rules, increasing the complexity of the decision tree. 

A problem is the decision tree begins to fit too closely to a specific set of instances. This is called **overfitting**, which is when the decision tree loses its ability to classify new data instances. 

If the model is not trained enough though, the inducted decision tree will be too simple to classify instances accurately, a concept called **underfitting**. 

The successfully accurate decision tree is a classifying model that has the ability to generalize - avoids overfitting and underfitting. 

Another problem is when the decision trees include branches that represent outliers, or noise, in the input dataset. It is common to apply some **pruning** method to remove these branches to improve the classification accuracy when being applied to new samples.

Success of the decision tree classifier is its ability to encode the decision-making knowledge in the form of decision rules. Other classifiers, like support vector machines and neural networks, are black box classifiers. 

Another advantage is their independence on the statistical distribution of the input data. 


## 5.2 - Decision Tree Approaches for Classification...

Most popular decision trees are:
- ID3
- C4.5
- CART

The approaches differ in the way features are ranked and selected while creating the decision tree. Also with respect to utilized pruning mechanism. 

Popular feature-ranking techniques used in decision tree approaches are:
- information gain;
	- used by ID3 approach.
- gain ratio;
	- used by C4.5 approach.
- Gini index;
	- used by CART approach.

### 5.2.1 - ID3 and Information Gain

**Entropy**: Generally speaking, the entropy is the degree of disorganization and randomness in a set of observations.

**Iterative Dichotomiser** (ID3) uses **information gain** (IG) to select the best splitting features. 

Information gain (IG) characterizes the distribution of the class data into a feature vector. 
- It measures the degree of homogeneity of the classes induced by a decision node. 
	- i.e.; a split of feature values. 
- Calculation of the IG of dataset features is based on measuring the **entropy** of the class assignments with respect to a split in that feature. 
- Quantity is inversely proportional to IG.
	- i.e.; information gained is the reduction of entropy of class assignment based on the feature split under examination. 

We now clarify concept of entropy. Suppose we have 3 sample sets of objects.
- Set A. has its objects equally divided between the two existing classes.
	- Therefore; the entropy of this set is one!
- Set B. has is *less impure* - or more pure - in that it has more of one class than the other. 
	- It has, therefore, less disorder, and entropy value between 0-1. 
- Set C. is completely *homogeneous* - it only has one class of objects in it. 
	- It has no disorder, and therefore, an entropy value of 0. 

The entropy value of dataset $D$ is represented by the function $Info(D)$. This function measures how the class labels in this dataset can partition its instance. Let the number of class labels in dataset $D$ be $m$. Then, the entropy of this dataset is calculated as follows:

$$
\tag{1}
\text{Info}(D) = \sum_{k=1}^{m}{\left( 
-P_k \cdot \log(P_k)
\right)}
$$

where $P_k$ is the probability that any instance in the dataset $D$ belongs to class $k$. 

The probability that an instance belongs to a class is calculated as the ratio between the number of instances that belong to $k$, and the total number of instances in $D$. 

The entropy of a dataset $D$, whose instances are partitioned by a feature $f$, is represented by the function $\mathtt{Info}_f(D)$. It is a function to measure the ability of any feature to split the dataset into equally divided partitions, where each partition corresponds to a single class label. 

A feature $f$ partitions the instances in the dataset into $v$ subsets, considering that this feature is of $v$ distinct values. 

Instances of each subset $d_i$ has the same value of feature $f$. The function $\mathtt{Info}_f(D)$ is calculated as the weighted sum of the entropy of the $v$ subsets, as follows:

$$
\tag{2}
\mathtt{Info}_f(D) = \sum_{i=1}^{v}{\left(
\frac{|d_i|}{|D|} \cdot \mathsf{Info}(d_i)
\right)}
$$

Function $Info(d_i)$ represents the entropy of subset $d_i$. Term $\frac{|d_i|}{|D|}$ acts as the weight of the partition. The value of $|d_i|$ is the number of instances in said partition. And the D is the total number of instances. 

The entropy in the dataset is reduced from $Info(D)$ to $Info_f(D)$ when a feature $f$ splits the instance in $D$. The reduction in the entropy due to specific features is equivalent to the information gain of this feature. 

The information gain of feature $f$ is represented by function:

$$
\tag{3}
\mathsf{Gain}(f) = \mathsf{Info}(D) - \mathsf{Info}_f(D)
$$

The information gain of a feature in *inversely* proportional to entropy of the dataset when this feature is used. The feature divides the dataset into a group of subsets. If all the values of this feature are distinct, then each subset includes only one instance. Accordingly, the information gain is calculated for discrete features only. 

### 5.2.2 - C4.5 and Gain Ratio

p. 113

**Information Gain** technique provides a higher-ranking value to the features having values that are more distinct. 
- Reason for behaviour is (typically) the purity of the corresponding partitions is high.
- Illustrate a point with a problem. 
	- Something about entropy of feature is zero since the partition is homogenous. 
	- splitting the tree based on this feature does not yield high information gain. 
	- using an ID-field for classification is a poor choice. 

The C4.5 approach handles this *problem* by normalizing the $gain(f)$ to form a new value, $\text{gainRatio}(f)$. The ranking measure is states as:

$$
\text{gainRatio}(f) = \frac{\text{gain}(f)}{\text{SplitInfo}(f)}
$$

Let the term SplitInfo be the normalizing factor that is inversely proportional to the ranking measure `gainRatio(f)`. The calculation is based on the average sum of the ratio between two numbers: 
- $|d_i|$
	- number of instances in the ith partition among the $v$ splits of partitioned by a feature $f$. 
- $|D|$
	- the total number of instances in the dataset

Let;

$$
\text{SplitInfo}_f(D) = \sum_{i=1}^v{
\left( \frac{|d_i|}{|D|} \cdot \log{\left(\frac{|d_i|}{|D|}\right)} \right)
}
$$

The value of `SplitInfo(f)` decreases as the number of instances in each partition decreases with respect to the total number of instances. However, if approaching the zero value, this leads to an unstable ranking measure because you cannot divide by zero.

C4.5 algorithm has other advantages over the ID3 algorith:
- It can deal with both continuous and discrete features.
- it handles missing values and applies tree pruning after the process of the tree induction. 

### 5.2.3 - CART and Gini Index

The gain ratio ranking technique provides a high rank to the features that split the dataset into *unbalanced partitions*. 
- If a partition splits the dataset quite unequally - it has high rank. 
- partition being larger than the other.

The CART decision tree classifier uses the Gini Index `Gini(D)` to measure the **impurity** in the dataset of instances - just say dataset.

Rank of any feature $f$ is measured by the amount of reduction in impurity. The reduction occurs when the feature is used in binary, splitting the instances into two partitions. 

The feature that maximizes the impurity reduction is selected as an important feature for the classification problem. 

The rank $\Delta Gini(f)$ of feature $f$ is calculated as the difference between the Gini index $Gini(D)$ of the total dataset of instances and the Gini index $Gini_f(D)$ of the datasets partitioned by this feature. 

The impurity reduction is calculated as:

$$
\Delta Gini(f) = Gini(D) - Gini_f(D)
$$

Where $Gini(D)$ represents the impurity in a dataset $D$ and calculated as:

$$
Gini(D) = 1 - \sum_{k=1}^{m}{P_k^2}
$$

We let $P_k$ be the probability that an instance in the dataset belongs to class $k$ in the $m$ classes of $D$. 

Again, the Gini impurity index $Gini_f(D)$ considers only a binary split for feature $f$ in $D$. The selected splitting point is a value in the feature vector $f$ that is best at splitting the instance in $D$ into two partitions $d_1$ and $d_2$ only. 

The value of $\text{Gini}_f(D)$ calculates the weighted sum of the impurity in each of the two sets as follows:

$$
\text{Gini}_f(D) = \frac{d_1}{D} \text{Gini}(d_1) + \frac{d_2}{D}\text{Gini}(d_2)
$$

### 5.2.4 - Example on Information Gain Calculation for ID3

The course book begins an example of a database with 14 customers to a computer shop. Each customer has 4 characteristics: age, income, graduation, credit rating. The store classifies each customer as buying or not buying a computer. 

Table 11 on page 115 gives example data. None of the data is simple integer values, even age. That is: young, middle, old. 

Then we begin with partitioning data, 9 instances of buys computer, and 5 of not. The entropy:

$$
\begin{align}
\text{Info}(\text{CShop}) &= \text{Info(yes, no)} \\
&= Info(9,5) \\
&= (9/14) \log_2(9/14) + -(5/14)\log_2{(5/14)} \\
&= 0.94
\end{align}
$$

Then we calculate the entropy of values of the feature age:

$$
\begin{align}
\text{Info}(\text{CShop}_{\text{young}}) &= \text{Info(yes \& Young, no \& Young)} \\
&= Info(2,3) \\
&= (2/5) \log_2(2/5) + -(3/5)\log_2{(3/5)} \\
&= 0.971 \\
\text{Info}(\text{CShop}_{\text{middle}}) &= \text{Info(yes \& Middle, no \& Middle)} \\
&= Info(4,0) \\
&= (4/4) \log_2(4/4) + -(4/4)\log_2{(4/4)} \\
&= 0.0 \\
\text{Info}(\text{CShop}_{\text{old}}) &= \text{Info(yes \& Old, no \& Old)} \\
&= Info(3,2) \\
&= (3/5) \log_2(3/5) + -(2/5)\log_2{(2/5)} \\
&= 0.971 \\
\end{align}
$$

And then the entropy of feature age is calculated as the weighted sum of the entropy of all possible values of the feature. 

$$
\begin{align}
\text{Info}_{age}(\text{CShop}) &= \left(\frac{5}{14}\right) \cdot 0.971 + \left(\frac{4}{14}\right) \cdot 0.0 + \left(\frac{5}{14}\right) \cdot 0.971 \\
& = 0.694
\end{align}
$$

The information gained from partitioning the dataset according to the feature age $Gain(Age)$ is calculated as:

$$
\begin{align}
Gain(Age) &= Info(CShop) - Info_{age}(CShop) \\
&= 0.94 - 0.694 \\
&= 0.246
\end{align}
$$

The book nicely gives us the other features:
- $age = 0.246$
- $student = 0.151$
- $income = 0.029$
- $credit_rating = 0.048$

We see that age is considered as the feature of the highest information gain and thus expected to act as the best splitting feature. 

The feature in the dataset CShop are sorted according to their importance as follows: age, student, credit rating, and income. 

## 5.3 - Decision Tree for Regression

**Regression**, in an ML sense, is a method of predicting the numerical value of a target variable given one or more independent variables. 

A decision tree for **regression** can be constructed by an ID3 algorithm that uses the standard deviation reduction method instead of the information gain method. The standard deviation is a measure of the degree of variation in a set of numerical values. 

A feature vector of similar values is considered homogenous. The standard deviation of a completely homogenous feature vector is zero. 

We now consider a dataset with two feature vectors of "Day", and "Temp" with a target variable of "Target". We are tasked to create a regression model by using a decision tree to predict the value of the target variable "Target" based on the feature vectors (predictors). 

Page 117 has a table of data with days, temperatures as "hot", "mid", and "cold". The class, or target, variable in a regression problem is a vector of numerical values. It is not categorical ones as in the previously considered classification problem. 

For our case, the $n = 14$ values has average $\bar{c} = 25.21$. Standard deviation is:

$$
\sigma_c = S_c = \sqrt{\frac{\sum(c - \bar{c})^2}{n}} = 17.07
$$

Now we consider the standard deviation of $S(c,x)$ of the target vector $c$ partitioned based on the feature vector $x$. 

The feature $x$ is a categorical variable of three discrete values, while each value $v$ is corresponding to a subset of values in $c$. 

Let the $P(v)$ refer to the probability of $v$ occurring in the target vector $c$. Its value is equal to the ratio of the number of instances whose value is $v$ to the total number of instances. The standard deviation $S(c,x)$ is calculated as:

$$
S(c,x) = \sum_{v \in x}{P(v) \cdot S_c(v)}
$$

Table 2 on page 118 shows all the stats. Looks like the total standard deviation is the sum of the... is the function above. 

The reduction in standard deviation is evaluated as the decrease in the standard deviation $S(c)$ of the target feature when the instances are split by a feature vector $x$. This results in standard deviation of $S(c,x)$. The value of the reduction in standard deviation is then calculated as:

$$
\tag{4}
SDR(c,x) = S(c) - S(c,x)
$$

That is the **Reduction in Standard Deviation**. In this example we have:

$$
\begin{align}
S(c,x) &= \sum_{v \in x}{P(v) \cdot S_c(v)} \\
&= 3.091 + 5.263 + 5.456 \\
&= 13.810 \\
SDR(c,x) &= 17.07 - 13.81 \\
&= 3.26
\end{align}
$$

This reduction in the standard deviation $SDR$ of the target vector is measured for each feature. The features are ranked based on the SDR value, such that the feature whose SDR value is the is  considered the most important feature.

The coefficient of variation $CV$ is then calculated, which is the "percentage ratio" of the standard deviation $S$ to the mean value $\bar{x}$ of a feature $x$. 

The $CV$ (coefficient of variation) is used to stop the branching in the decision tree induction process. The value of $CV$ is calculated as:

$$
\tag{5}
CV = S/\bar{x} \cdot 100\%
$$

Which in our case is $\approx 67\%$. 

## 5.4 - Decision Tree Construction

p. 118;

Note that the decision tree in the three previously mentioned approaches (ID3, C4.5, and CART) were constructed in a **greedy**, top-down manner. The algorithm pertaining to these approaches uses a recursive function to iterate over the set features. 

First, the algorithm selects the highest ranked feature (greedy) from the feature set. A root-node is created to represent this feature, which is also removed from the list of features to consider in the next iteration. 

Branches are created down for this parent node (top-down), with each branch labeled by a distinct value (or range of values) for the corresponding feature value. 
- If the instances in the input dataset that have this specific feature value are of different class labels; 
	- Then the next highly ranked feature is selected to the added as a child decision node from this branch. 
- Else-if all the instances of this feature value are of the same class $C$,
	- Then the child node from this branch is a leaf node that is labeled by this class $C$. 

A node that represents a feature is called a **decision node**. A node that represents a class label is represented as a **leaf node**. 

The process continues recursively until all terminal nodes of the tree are *leaf nodes*. 

#### 5.4.1 - The Decision Tree Creation

We now present the steps of the tree induction in the ID3 algorithm. 

Suppose we are creating a function to construct a decision tree called `BuildTree()`. The function is recursive and has two input parameters. The first is the input dataset and the second is the set of attributes. The output of this function is a decision tree that describes the classification rules of instances in the dataset $D$. 

```rust
fn buildTree(dataset: DataSet, features: Features) -> DecisionTree {
	let node: Node = createNode();
	
	// all instances belong to same class C_i
	if (Info(dataset) == 0) {
		return node; // return node N as leaf node with class label C_D
	}
	if (isEmpty(features)) {
		// return node N as leaf node with classs label C_m
		// for majority of instances in D.
		return node;
	}
}
```

That was a fun attempt but the Pseudo code isn't built for Rust. Here are the steps for function `BuildTree(D, A)`:
- Create node `N`.
- If `Info(D) == 0`, where all instances belong to the same class $C_1$:
	- Returns the node $N$ as a leaf node with class label $C_D$. 
- If $|A| = 0$, where $A$ is empty:
	- Returns the node $N$ as a leaf node with class label $C_m$ for the majority of instances in $D$.
- The rank of each feature $f$ in the input dataset $D$ is (re-)calculated. The ID3 algorithm operates on features of discrete values only. A discretization process is applied to features of continuous values in the pre-processing step. 
- Select the feature $f$ of the highest rank from the set of features in $A$.
- Label node $N$ as a decision node for feature $f$:
	- Create a branch output from the node $N$, and label the branch by the condition $f = x$.
	- Construct a subset of instances $D_{f = x}$, where the value of feature $f$ of the instances in $D_{f=x}$ is $x$. 
	- If $D_{f = x}$ is not empty:
		- Call recursively $BuildTree(D_{f=x}, A-f)$.
			- Remove feature $f$ from the set of features $A$.
	- ELSE
		- Add leaf node and label this node with class label $C_m$ for the majority of instances in $D$. 

##### Example

We consider the same dataset as we did in the previous section. Now it is `BuildTree(CShop, Age, student, credit_rating, income)`. The function selects a feature as the root node of three branches.

Suppose it selects `Age`. The `BuildTree()` function is called recursively three times then for each branch, the branches being: `Young`, `Middle`, `Old`. 

Suppose we start at "Young", the function is

$$
\text{BuildTree}(\text{CShop}_{\text{Age}=\text{Young}}, \ \{ 
\text{student}, \
\text{credit\_rating}, \
\text{income}
\})
$$

This is called recursively:
- The Entropy `Info(D)` of input dataset $CShop_{Age=young}$ is calculated;
- The ranking information `gain(f)` of each feature $f$ is re-calculated. 
- The best-ranked splitting feature is chosen
	- suppose it is "student" in this walk-through. 
- The corresponding node is created.
	- For "student", we have two output branches, either "yes" or "no". 

Then the process continues for something like:


$$
\text{BuildTree}(\text{CShop}_{\text{Age}=\text{Young} \ \& \ \text{Student}=\text{Yes}}, \ \{ 
\text{credit\_rating}, \
\text{income}
\})
$$

For both recursively called functions, both datasets for Age is "Young" and Student is "Yes" or "No" return leaf nodes. (might need to double check that....)

We would continue for where the Age is "Middle" and "Old" as well, just to help remember:
- We call the recursive function `BuildTree()`
	- For datasets like `cshop_age_is_middle` and `cshop_age_is_old`
- We calculate the $Info(D)$ of the dataset.
- We calculate the $gain(f)$ for each *feature*. 
- The best ranking feature is the new split.

In our example, we supposed if Age is "Young", the next best ranking feature is Student. However, that does not need to be the same across the board. For Age is "Middle", the next best ranking feature could be "Income". 


## 5.5 - Decision Tree Pruning

Generally, the complexity of the decision tree increases as the size and heterogeneity of the input dataset increases. 
- [Heterogeneity | merriam-webster.com](https://www.merriam-webster.com/dictionary/heterogeneity) : the quality of state of consisting of dissimilar or diverse elements.
	- State of being *heteregeneous* - consisting of dissimilar or diverse ingredients or constituents
	- i.e.; mixed
- [heterogeneity | dictionary.cambridge.org](https://dictionary.cambridge.org/dictionary/english/heterogeneity#google_vignette) : the fact of consisting of parts or things that are very different from each other. 
- [heterogeneity | thefreedictionary.com](https://www.thefreedictionary.com/heterogeneity) : The quality of being heterogeneous / of being made of many different elements, forms, kinds, or individuals. 

So you need more data and the data needs to be different to increase complexity. 

This is particularly valid when data contains noise and outliers. 

Decision trees with many decision rules will be complex and hard to interpret. Complexity may increase to the point of causing an overfitting problem. 

**Overfitting** occurs when the rules incorporated by the decision tree fit the limited set of training instances *perfectly*. However, they fail to *reliably* classify new instances (from data outside the training dataset). 
- This problem decreases the performance of the decision tree classifier.
	- I don't think performance means *speed* in this case, but more like accuracy. 

**Tree Pruning** helps address the problem of overfitting by decreasing the size of the tree, which makes it less complex. 

There are many pruning techniques. One we will discuss here works as follows:
- Remove subsections in the decision tree that have low classification power. 
- The low degree of discriminating power is measured against an arbitrary threshold.
	- If a section's discriminating power is below the threshold, then it is considered unnecessary. 
	- The threshold should be low to avoid pruning too much, making the tree very small and too trivial to sufficiently classify new instances. 
		- This creates the problem of **underfitting** - basically the model just sucks - it wasn't able to learn from the training data.

Tree pruning techniques can be applied either in:
- **Pre-pruning**:
	- Avoids building up low-discriminating sections while the decision tree is being constructed. 
	- When a condition is met:
		- The tree constructing algorithm avoids adding a new decision node to split the instances among the resulting branches. 
		- It instead adds a leaf node with the label of the most frequent class among the pretraining instances.
	- The concrete form of the pruning condition depends on the feature-ranking measure used in the decision tree induction. 
	- Information gain, gain ratio, and Gini Impurity index measures can all be used to gauge the impact of adding the decision node in question. 
	- And if the used ranking is below the arbitrarily specified threshold, then further partitioning is halted. 
- **Post-Pruning**:
	- This removes spurious sub-trees from the already fully constructed decision tree and replaces them with leaf nodes with the label of the most frequent class among the sub-tree. 
	- The CART approach implements the post-pruning process. 
		- It measures **cost complexity** of the tree for each decision node in a bottom-up manner.
			- **Cost Complexity** is a function of the number of leaves and the rate of error (misclassified instances) in the tree.
		- If the cost complexity of the tree increases by replacing a decision node with a leaf node, then the descendant sub-tree of this decision node is pruned. 

## 5.6 - Decision Tree in Ensemble Methods

p. 123;

An **Ensemble Method** is meta-method that combines a series of machine learning algorithms to improve the learning performance.

[Ensemble Learning | Geeks for Geeks](https://www.geeksforgeeks.org/machine-learning/a-comprehensive-guide-to-ensemble-learning/) is a method where we use many small models instead of just one. The models may be weaker, but combining the results gives a more accurate answer. 

Sounds like the sum of the parts is greater than the whole. 

Learning algorithms used are **base learners** and are often **weak learners**. 

A **Weak Learner** is a poor learning algorithm that performs slightly better than a random classifier. Error rate of the results of this classifier is nearly 50% for binary classification problems. 
- A decision tree can be used as a weak learner by controlling its maximum depth. 
- A decision tree of one level (*decision stump*), or a shallow decision tree, can be used as a weak classifier. 

The main principle behind ensemble methods is that instead of training a single strong classifier on the whole input space, it is better to train many weak base-classifiers that are good at different parts of the input space. 

The aggregated base classifiers are either:
- A single learning algorithm, like decision trees (**homogeneous** weak learners).
- Different learning algorithms (**heterogeneous** weak learners).

Two prominent types of ensemble methods of homogeneous weak learners are:
1. The bagging method.
2. The boosting method.

An example of an ensemble method of heterogeneous weak learners is:
1. The Stacking method. 


The bagging method, aka bootstraping method, is an aggregation ensemble method for  homogeneous weak learners. 

**Bootstrapping** refers to the method of generating bootstrap samples. These are sample that are subsets of a specific number of instances $x$ that is less than the total number of instances $X$. 

I feel like we might get steps to an algorithm here:
- An initial subset of $x$ instances is generated.
- Then $n$ subsets are generated by random drawing and replacement of instances. 
- Each of the $n$ subsets are used to form a decision tree.
	- They are controlled to be a decision stump or a simple shallow-depth decision tree. 
- This bagging method is trained to build $n$ weak learners. 

When classification of new instances, each instance is tested by each of the $n$ weak learners. The outcome of each weak learning is like a vote to one of the class labels of the problem. 

Something about the resulting vote being determined by calculating the average (mean) voted class labels. This step gives equal weight to each vote, yielding an unweighted average because the homogeneous weak learners are formed independently and in parallel. 

[ML Bootstrapping Explained | Baeldung.com](https://www.baeldung.com/cs/machine-learning-bootstrapping-explained) gives a short explanation. 

[Bootstrapping in Machine Learning | Applied AI Course](https://www.appliedaicourse.com/blog/bootstrapping-in-machine-learning/) Cover the details and goes over the Iris data set. So you get an example in Python with SciKit Learn. 

[Bootstrap Aggregating | Wikipedia](https://en.wikipedia.org/wiki/Bootstrap_aggregating) also covers Random Forest, which we discuss below. 

The **Random Forest** method is another example of a bagging method. It is similar to Bootstrapping but with a change in the *bootstrapping* step. 

The steps from above:
- An initial subset of $x$ instances is generated.
- Then $n$ subsets are generated by random drawing and replacement of instances. 
	- The instances of each sample have a random subset of $m$ features rather than the original set of features $M$. 
	- So, generates $n$ samples of $m$ features
- Each of the $n$ subsets are used to form a decision tree.
	- They are controlled to be a decision stump or a simple shallow-depth decision tree. 
- This bagging method is trained to build $n$ weak learners. 

The two main advantages of the $n$ samples with $m$ features are:
1. This enables the *forest* to efficiently handle a high number of features (dimensionality) in a problem.
2. This reduces the correlation between the predicted class label from highly different learners. 

[Random Forest Algorithm in Machine Learning | Geeks for Geeks](https://www.geeksforgeeks.org/machine-learning/random-forest-algorithm-in-machine-learning/)

And now the term "Random Forest" makes sense because of all the decision *trees*. 

In the **Boosting Method** the performance of the homogeneous weak learners is updated by the training samples iteratively. The boosting *technique* is based on the bagging method, except that it applies a **sequential fitting** of the formed learners in an iterative manner. 

Each learner is fitted by giving **more weight** to instances that were incorrectly classified in the previous iteration. 

The first iteration in the boosting method performs just like the bagging method: The probability of selecting any instance in the formed samples is equal for all instances in the dataset. 

In the first iteration, each instance is provided with an initial weight of $1 \over k$, where $k$ is the number of class labels in the dataset. 

Then in the next iteration, the weight of misclassified instances if updated by increasing its value. The instance of higher weight has a higher chance, or probability, of being selected in the samples. 

The performance of the ensembles method should be increasing at each iteration where the learners of the model are fitting more instances correctly. 

The iterative model continues until a stopping condition where the performance of the method is not rising anymore. 

The stopping condition is dependent on the domain problem. 

For example, it is sufficient to have some maximum accuracy threshold. 

Boosting methods may risk overfitting because of the focus on misclassified instances that may be outliers or noise!

The **Adaptive Boosting**, or **Adaboost**, method is another example of the boosting methods. The Adaboost method assigns the higher weight to misclassified instances so that these instances receive the high probability for classification in the next iteration. Additionally, it also assigns the higher weights to the learners that shows a higher classification accuracy. 

Therefore, that vote of the learner of higher accuracy receives a higher weight in calculating the average vote. The final vote in the Adaboost method is weighted average of the votes of the learners, unlike the boosting method. 

Like the previous ensemble models, this iterative model continues until a stopping condition is met. 

The **gradient boosting** method is an Adaboost method that weighs based on a loss function. This loss function of each of the learners is the opposite of the gradient descent of the current fitting error. Another method is proposed based on the gradient boosting method, the **Extreme Gradient Boosting: XGBoost** The loss function of this method computes the second order gradient to provide more information to classifier and reaches higher accuracy. 

### Implementation in Python

Sample code provided for implementing the decision tree classifier using Python. We pretend to have a dataset:

```Python
import pandas as pd
from sklearn import metrics
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier

trial_data = pd.read_csv("./data/trial_dt.csv")
print(trial_data.shape)

# Data preprocessing
# 1.) Divide data into attributes and labels
x = trial_data.drop('buys_computer', axis=1)
y = trial_data['buys_computer']

# 2.) Divide data into training and testing sets
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.2)

# Processing of classifier 
clf = DecisionTreeClassifier()
clf = clf.fit(x_train, y_train)

# Predict the response for test data
y_pred = clf.predict(x_test)

# Model Accuracy, how often classifier is correct
print("Accuracy: ", metrics.accuracy_score(y_test, y_pred))
```

## Summary

Decision Trees represent a group of classification techniques that is based upon the construction of a tree like structure. Several approaches are proposed for construction decision trees like:
- ID3;
- C4.5;
- CART;

Decision tree classifiers use statistical-ranking techniques like information gain, gain ration, or Gini Impurity Index. 

These techniques help in identifying the important features to use in building the decision tree. The constructed tree is typically very complex, especially when large datasets with the high probability of noise are used. A pruning process is applied to simplify the decision tree and to avoid the possible occurrence of overfitting. Decision trees are commonly used in ensemble classification models because they are considered weak learners. 

