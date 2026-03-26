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

# Course Learning Objectives

pp. 12-13

The goal is to give you necessary knowledge about Machine Learning (ML) techniques and mathematical tools to take a *leading role* in a Data Science or Artificial Intelligence team.

Neural Networks and Deep Learning (DL) have become cornerstones of modern machine learning, and there's a Deep Learning course for that. Here we focus on other widely implemented machine learning techniques such as:
- Clustering
- Regression
- Support Vector Machines (SVM)
- Decision Trees
- Genetic Algorithms

Unit 1 will start with general overview to introduce field and nomenclature. We also look into reinforcement learning!

Then we look at different techniques and metrics to evaluate. 

Note: the book uses the Python ecosystem as the technical programming tool.

# 1. Introduction to Machine Learning

pp. 15-30

What will we learn?
- What is meant by *machine learning*.
- Common terms and definitions in machine learning.
- The different applications of machine learning.
- The concepts of Classification and Regression.
- The difference between each of the machine learning paradigms.
- How reinforcement learning is performed. 

## Introduction

The course book starts with discussing how data analytics can be used to find *patterns* when a company launches advertisement campaigns to determine what brings in the most revenue. 
- because this is how we should be making money...

Diving into purchase data, they find the *patterns* to determine what brings in the revenue, and to *predict* the type of customers who bought the most products or spent the most money. 

The purchase data collected can be vast, making it *intractable* by human or manual implementations - we cannot calculate statistics by hand. This is where machine learning tools are introduced to employ the high performance capabilities of a computer (i.e. machine) in handling this large amount of data (i.e. inputs), and develop a model that learns from the data to automatically and efficiently achieve both the pattern finding and prediction tasks (i.e. outputs).

The Challenge: Find an algorithmic description of the task that can be expressed in the form of a classical computer program based on the knowledge that we have concerning the domain. 

Instead of this, we collect a large amount of inputs and their associated outputs and then fit a *mathematical* model to define the relations between the inputs and outputs. We then utilize this model to predict outputs for new scenarios!

The developed model (discussed right above) is called a **machine learning** model. **Machine Learning** as a field of study is concerned with the question of how to construct computer programs that automatically improve their performance (P) from experience (E) with respect to some provided task (T). 

Machine learning uses a *computing device* to *process data*. 
- Inputs
	- Independent variables
	- Like data from product campaigns
- Associate outputs
	- Dependent variables or Target variables
	- Like revenue

A **model** can be thought of as a mapping of inputs to output, usually represented as a program. The model performs the pattern finding or prediction tasks. 

Machine learning is different from traditional programming. Traditional programming constructs an *explicit* process mapping inputs to a desired output with a set of code instructions. ML is a mathematical and algorithmic approach that builds a model from the given data to perform predictions or generate insights about new data scenarios. 

Data analytics task starts by *understanding* the data domain and applying necessary data integration, pre-processing, etc... Then the machine learning models are developed. Then the models are used and results are interpreted. Then the patterns and predicted outputs are presented. 
- There may also be some maintenance state I think.

Data is usually given as input/output pairs with no explicit relationships between them. ML can be thought of as the transformation of raw (often useless data) into meaningful information. ML integrates many mathematical tools:
- probability and statistics
- optimization
- control theory

Machine Learning models find application in many disciplines:
- vision processing
- language processing
- forecasting
- pattern recognition
- games
- data mining
- expert systems
- robotics

ML use cases cover many fields such as:
- Recognizing patterns for facial identification and emotion detection.
- Recognizing handwritten characters and speech.
- Recognizing objects of interest in medial images.
- Detection of motion in consequent images.
- Recognizing unusual credit card transactions, sensor readings, engine sounds, etc...
- Prediction of future stock prices or currency exchange rates.
- Detection of fraud and spam filtering.
- Establishing a recommendation system. 
- Grouping documents or images with similar contents.
- Dimensional reduction, (i.e.; make a set of high-dimensional data points amenable to visual inspection.)

Note: it's all about the DATA!

ML methods are used to find patterns within the inputs (independent variables) and/or to predict relationships between inputs and outputs (labels or dependent variables). 

Outputs of any dataset are either continuous or discrete values. 

ML prediction models for continuous outputs are called **Regression** models. For discrete outputs, we call these **Classification** models. The many approaches for building these models will be discussed later. 

What if we have data and we don't have target outputs? The goal is to discover hidden patterns within the data. ML techniques are used to perform a **Clustering Analysis**. This groups inputs into homogeneous clusters according to degree of similarity based on values of the given independent variables. 

Other types of analyses can be performed to detect outliers or to remove irrelevant variables and duplicated data (i.e.; dimensionality reduction). 

Generally, there are 4 main ML paradigms, each corresponding to a particular *abstract* learning task:
- Supervised learning
	- The learning task when data inputs and corresponding target outputs are provided.
- Unsupervised learning
	- concerned with discovering hidden patterns - includes clustering as important sub-domain.
	- Outputs are not known
- Semi-supervised learning
	- Covers problems where only partial label information exists.
- Reinforcement learning
	- This is a learning setup where the goal is to find an action policy that achieves a given goal. 
	- The model learns to achieve the goal by trial-and-error interactions with its environment. 

## 1.1 Classification & Regression

Start with the *classic* email spam discussion. This leads to typical classification problems:
- dataset is collection of labeled-data records
	- Inputs = independent variables
	- Outputs = labels / associated classes
- Objective = develop ML model to relate inputs to outputs
	- to predict class of new inputs. 

Classes should be *disjoint* - the model must assign a single class to inputs.

Usually the dataset is divided into two sets:
- Training 
	- Dataset used by ML model to build its predictive mathematical function.
- Testing
	- Dataset used to measure performance of developed ML model. 

For binary classification, outputs of the model can be presented in a confusion matrix form. 

Confusion matrix is this:

Top is "Model's Output" and Side is "Desired Output"

| n/a     | Class 1 | Class 2 |     |
| ------- | ------- | ------- | --- |
| Class 1 | TP      | FN      |     |
| Class 2 | FP      | TN      |     |

We boldly assume that Class 1 is the *positive* class, and Class 2 is the *negative* one.

Terms:
- True Positive (TP)
	- correctly classified by trained model to be Class 1.
- True Negative (TN)
	- correctly classified by trained model to be Class 2.
- False Positive (FP)
	- Wrongly classified as Class 1 (to be positive).
- False Negative (FN)
	- Wrongly classified as Class 2 (to be negative).

Classification metrics:
- Precision
	- Number of true positives over total assigned to be positive (as Class 1)
	- Considered a measure of *exactness*.
	$$
	Precision = TP / (TP + FP)
	$$
- Recall
	- Number of true positives over the total instances that are actually positive.
	- Considered a measure of *completeness*.
	$$
	Recall = TP / (TP+FN)
	$$
- F-Score
	- A weighted average of precision and recall
	$$
	\text{F-Score} = \frac{2( \text{Precision} \cdot \text{Recall})}{( \text{Precision} + \text{Recall})}
	$$

There are many techniques to develop classification models. Sometimes we employ several techniques in parallel and the one that returns the highest evaluation performance is selected. 

In Regression problems, the task is to develop and ML model to predict a value, not a class. Generally the developed model is a mathematical function that relates outputs to inputs. 

The evaluation metric usually calculated to judge model's performance is the **mean squared error (MSE)**:

$$
MSE = \frac{1}{n} \sum^{n}_{i=1}(y-d)^2
$$
Let:
- $y =$ output of developed regression model.
- $d =$  the desired output.
- $n =$ total instance - data.

In ML there's a trade-off between goodness of fit and complexity of the model. It is tough to develop an ML model with many variables and free parameters. The model becomes complex because it can use these degrees of freedom to *always* produce a good fit on the training data. 

Insufficient degrees of freedom can also degrade influence on its produced fit. 

Generally, more observations are better. However, too much *adaptability* will force the model to learn the noise within the training data rather than the underlying input/output relations.
- Results in **overfitting** the training data.
- Will perform worse on testing dataset. 

**Overfitting** happens when the model highly adapts to the training set, memorizing results instead of learning patterns. This impacts the degree of generalization to new data. 

**Underfitting** happens when the model does not capture enough of the inherent structure in the training data. This results in just poor performance overall. 

## 1.2 Machine Learning Paradigms

### 1.2.1 Supervised Learning

p. 21

**Supervised Learning**:
- the given dataset contains inputs and outputs.
- objective is to develop association model (f) that relates inputs to outputs.
- The model should predict outputs for future inputs.

Equations

$$
\begin{align}
y &= f(x_i) \\
i &= 1, \dots, n
\end{align}
$$

We let $n$ be the total number of variables (ie; characteristics) in the data samples. 
- function $f$ is an estimation of possible output for underlying $x_i$ variables.
	- classification - output belongs to a set of finite and discrete values; the predicted classes.
	- regression - output belongs to a range of infinite continuous values that define the numerical outcome(s).

How does training work?
- Parameters are continuously updated until the optimum setting is achieved.
- Parameter updating process is governed by a specific **loss function**. 
	- object = adjust parameters such that loss function is minimized.
	- For regression - loss function can be MSE.
	- For classification - can be number of wrongly classified instances.

The book provides a simple illustration. Then examples where maybe used:
- Previous home sales.
- Previous loans that were paid.
- Previous week's visa applications.
- Previous statistics of benign/malignant cancers.

Techniques:
- Linear classifier
- Linear regression
- Multi-Linear regression
- Support Vector Machine (SVM)
- Naïve Bayes
- Gaussian discriminant analysis (GDA)
- Hidden Markov Models (HMM)
- K-nearest neighbors
- Kernel regression
- Kernel density estimation
- Decision Tree

### 1.2.2 Unsupervised Learning

p. 23

Now we have a basic of things, no labels on the things. We just want to organize them into groups based on similarities. This is like the process of **Unsupervised Learning**. It is implemented for problems with unlabeled datasets. 

This can be common in practice because acquisition of labels is typically expensive in big data applications. 

The objective of unsupervised learning is to discover the salient patterns within the given inputs, which result in **dimensionality reduction** - a process of removing irrelevant variables from the dataset. Another result is clustering the data instances into groups based on similarities. 

Another illustration is provided. 

Unsupervised learning models learn to represent inputs by extracting statistical structure that is intrinsic to the overall collection of data instances. A good use case is for finding the best independent variables useful for visualizing or clustering the dataset. 

Unsupervised learning also encompasses identifying data points with high difference to the typical data points in a given dataset... That is; finding **outliers** - a term that refers to those data records that are far from the bulk of the input dataset. 
- True outliers
	- Actual outliers from data generating process.
- Fake outliers
	- Stem from measurement, recording, or data storage errors.
	- Think human error.

The **cost function** can be the:
- minimum quantization error;
- minimum distance between similar data instances;
- maximum likelihood estimation of correct cluster.

Example use cases:
- Discover patterns in customer profiles - are customers similar?
- Anomaly detection of financial transactions.
- Are products typically purchased together?

Common techniques:
- K-means
- Hierarchical clustering
- Gaussian mixture model (GMM)
- Graphical models
- DBSCAN
- Principal component analysis
- factor analysis

### 1.2.3 Semi-Supervised Learning

p. 25

**Semi-Supervised** learning is for datasets where the output is given for only a few instances of the inputs. Basic classification model is designed on a few labeled data instances; the semi-supervised classification/clustering step. 

Then the model is tuned up to operate without supervision on the remaining large unlabeled data instances - assigning the classes from the first step. The second step is to transfer labels to all samples. 

The main advantage is the effort and computational costs saved from not performing the expensive manual process of collecting and labeling large datasets. It can also bring more insights into the dataset structure as patterns and similarities are discovered. 

A great application is in the field of medical imaging. 

## 1.3 Reinforcement Learning

p. 27

**Reinforcement Learning** deploys an agent in an environment to accomplish some task. It performs actions and receives rewards. 

The agent performs an action in an environment and receives a reward $r_i$ and moves into state $S_i$, where ($i$) represents the iteration. The process is repeated until the agent achieves the maximum reward. 

It is learning from sequential decision making. The model is simply given a goal to achieve and it learns how to achieve the goal by trial-and-error interactions with its environment. 

The building blocks of reinforcement learning setting are here:
- Agent 
	- hypothetical entity that performs actions in an environment to gain some reward.
- Action (A)
	- all possible moves that the agent can take.
- Environment (E)
	- Scenario that the agent has to face.
- State (S)
	- Current situation returned by the environment.
- Reward (R)
	- An immediate return sent back from the environment to evaluate the last action by the agent.
- Policy ($\pi$)
	- Strategy that the agent employs to determine the next action based on the current state.
- Value (V)
	- The expected long-term return of the current state under policy.

Reinforcement learning accomplishes ML by following the *cause and effect* method. The developed reinforcement model learns by performing an action in the environment that results in a maximum reward over a time horizon. Actions are adjusted until maximum reward is achieved. 

The **reward function** acts as the feedback to the agent as opposed to the set-up in supervised learning. 

The widely applied approach to perform a reinforcement learning is the model-based approach:
- The agent learns a model using few interactions with environment.
	- Agent starts at state $S_1$
	- Agent takes action $a_1$
	- Agent reaches $S_2$ and gains reward $r_2$
	- etc...

The advantage of the model-based approach is the speed-up of the learning phase because no need to wait for environment to respond, nor reset the learning process to its initial state. 

Applications include:
- gaming
- robotic movement control

## Summary

p. 29

Machine Learning (ML) is an inductive process that automatically builds a prediction model or extracts relevant patterns by learning the natural structure of a given dataset. 

Four paradigms are supervised, unsupervised, semi-supervised, and reinforcement learning. Each paradigm is characterized by the kinds of data they require, output generated, the algorithms used to arrive at the learned model. 
