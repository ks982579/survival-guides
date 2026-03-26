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

https://courses.dwf.dev/docs/reference/docusaurus/katex
# 4. Support Vector Machines

pp. 87-106

We will learn:
- About the support vector machine (SVM) Model.
- What is meant by the term **hyperplane** and how it is represented. 
- The difference between linearly and nonlinearly separable data.
- What the kernel function is and how it is used in the SVM algorithm.
- What is meant by the *kernel trick*.

## Introduction

**Real-life data** are retrieved from different sources like sensors, surveys, and observations in practical application scenarios.

• Support Vector Machine (SVM) is a supervised machine learning algorithm.  
• SVM is known for its high discrimination power in decision-making applications.  
• The algorithm is capable of accurate classification and prediction.  
• It can handle both continuous and categorical data.  
• SVM can solve linear and nonlinear problems effectively.  
• The model is applicable to various real-life situations.


## 4.1 - Introduction to Support Vector Machines (SVM)

p. 88;

- The SVM algorithm is a binary classifier that categorizes entities into two output classes.  
- Entities are represented as points in a multi-dimensional space, with each dimension corresponding to an entity's properties.  
- The two distinct classes correspond to different subspaces within the feature space.  
- These subspaces can be separated by a hyperplane, which has one dimension less than the feature space.  
- The hyperplane represents the boundary between the classes and is learned during the training phase.  
- During testing, the algorithm classifies new, unlabeled instances based on their position relative to the hyperplane.  
- For example, in a two-dimensional feature space (X,Y), a non-labeled instance is classified according to its proximity to the learned hyperplane.

Subspaces can be separated by a subspace that has one dimension less than the overall feature space. So if our feature space has 2 dimensions, it is a plane. Then our subspace separator is a line. If the features space has 3 dimensions, like a volume, then our separator becomes a plane. 

The subspace is the separating **hyperplane**. Classification puts a thing one either side of the hyperplane. 

The hyperplane, probably a formula, is determined during training. In the application phase, classification is based on the location of the data point corresponding to the instance, relative to the learned hyperplane. 


|          /
|       /
|    /
| /
 \_ \_ \_ \_

Pretend we have a hyperplane that is just a line. 
- The *gap* between the line of the hyperplane and the nearest instance of the different classes is known as the **margin** of the hyperplane. 
- The *closest* instances that determine the **margin** are defined as the **support vectors**. 
	- These vectors *support* the separating hyperplane. 

The goal of the SVM algorithm is to detect (or learn) the hyperplane that *maximizes* the width of the margin. 
- Width of the margin is measured based on the perpendicular distance from the separating hyperplane to the support vectors. 
- The algorithm is memory efficient
	- it uses only a subset of training points (support vectors) in the classification of the testing instances. 

The large margin ensures good genearlization of the classifying algorithm in discriminating between the instances of the two classes. 

### 4.1.1 - SVM Example 

We consider a problem represented in 2D space of X-axis and Y-axis. We have 6 data points. Each class, of the two classes, contains 3 of the data points. 

It's shown with graphs how the optimal hyperplane is found. 

Looks like the width is:

$$
w = \sum_{i=1}^n(M_i)
$$

### 4.1.2 - The Hyperplane

The **hyperplane** in SVM forms a space that separates the instances of different classes.
- Hyperplane is:
	- A straight line if the space is 2D.
	- A plane in 3D space
	- etc...

I.E., in n-dimensional space the hyperplane constitutes an $(n-1)$-dimensional subspace. 

Real-life problems usually are characterized by hundreds of features, making these settings impossible to visualize. 

## 4.2 - SVM for Classification

p. 91;

- The SVM classifier is a linear binary classifier, referring to its operation involving two categories of instances.  
- Each new instance x lies on one side of a hyperplane, defining the separation needed.  
- "Linear" indicates SVM's application to linearly separable problems, where a hyperplane is constructed using a linear equation.  
- Real-world data is often not linearly separable, necessitating curved lines or planes for effective separation.  
- Further explanations on how SVM manages non-linearly separable cases are discussed in later sections (Schölkopf & Smola, 2001).

- [What are SVMs | IBM](https://www.ibm.com/think/topics/support-vector-machine) - IBM has a good amount of information on their website. 
	- A **support vector machine (SVM)** is a **supervised** machine learning algorithm that classifies data by finding an optimal line, or hyperplane, that maximizs the distance between each class in an N-dimensional space. 
	- Widely used in ML as it can handle both linear and nonlinear classification tasks. 
		- Non-linearly separable data requires kernel functions to transform the data higher-dimensional space to enable linear separation. 
		- This is known as teh **kernel trick**
- [Support Vector Machine Algorithm | Geeks for Geeks](https://www.geeksforgeeks.org/machine-learning/support-vector-machine-algorithm/)
	- **Kernel** = A function that maps data to a higher-dimensional space enabling SVM to handle non-linearly separable data.
	- **Hard Margin** = A maximum-margin hyperplane that perfectly separates the data without mis-classifications.
	- **Soft Margin** = allows some mis-classifications by introducing slack variables, balancing margin maximization and mis-classification penalties when data is not perfectly separable. 
	- **Hinge Loss** = A loss function penalizing mis-classified points or margin violations and is combined with regularization in SVM.
	- **Dual Problem** = involves solving for Lagrange multipliers associated with support vectors, facilitating the kernel trick and efficient computation.

### 4.2.1 - Linearly Separable Problems (Hard Margin)

An SVM algorithm searches for a hyperplane that maximizes the margin between binary labeled instances.
- Note - labeled? - the IBM article states it IS a supervised ML algorithm. 

In the case of linearly separable instances:
- a separating hyperplane without training errors, or a hard margin, can be detected. 

The SVM algorithm uses the training instances to construct the linear function of the hyperplane. The goal is to use that description of the hyperplane to construct a function that maps each training instance $x$ to a function value $f(x)$ for which holds that $f(x) > 0$ for instances of one class, and $f(x) < 0$ for members of the other classes.

Let's consider a one-dimensional separation, a line. The genearl equation of a (straight) line is:

$$
f(x) = m \times x + b \tag{1}
$$

The constant $m$ is the slope, the book calls it $w$. 

Note the following

$$
\begin{align}
m &= w = \frac{\Delta y}{ \Delta x} \\
b &= y - \texttt{intercept}
\end{align}
$$

For a dataset of multiple features, the decision function $f(x)$ is a linear combination of the $n$ features $(x_1, x_2, \dots, x_n)$. These $n$ features represent a single instance $x$ in the dataset. 

The value of the instance $x$'s features are mapped linearly to the decision value $f(x)$ in analogy to equation 1. Let us look below at equation 2. 

$$
\tag{2}
\begin{align}
f(x) &= w_1 \cdot x_1 +  w_2 \cdot x_2 + \dots + w_n \cdot x_n +b \\
&= \sum_{i=1}^n w_i \cdot x_i + b \\
&= w \cdot x +b
\end{align}
$$

Here the final form is actually the **dot product**. We use $w$ instead of $m$ to better represent that they stand for the **weight** vector that describes the linear function of the SVM's hyperplane. This is a normal vector to the separating hyperplane.

Any point on the hyperplane has a decision value $\{ f(X) = 0 \}$ since this point cannot be classified in either of the two sides of the plane. 
- In training phase:
	- The decision value of any instance is either
		- $\{ f(X) > 0 \}$ if the data point of the instance is on one side of the hyperplane;
		- $\{ f(X) < 0 \}$ if the data point lies on the other side of the hyperplane. 

Determination of the hyperplane linear equation (2) requires the calculation of the weight vector $w$. 

Input to the SVM classifier is a training set of $m$ pairs $(x_i, y_i)$ (I don't know why they use such unusual variables...), such that each instance $(x_i)$ has a known label $(y_i)$. The class label has two possible values, $\{ 1, -1 \}$. 

The required output of the training phase is the calculation of the $w$ vector and the displacement $b$. 
- This is, a vector is actually a composition of many values, and then $b$. 

These values are calculated such that the margin between the support vectors is maximized by this specific hyperplane. 

The separating hyperplane lies between parallel **marginal hyperplanes**, right in the middle. 
- Each marginal hyperplane is supported by a set of critical training instances (support vectors) that lie on it. 
- Since rescaling the feature sample does not change their linear separability, we can transform the input data in such a way that our classification function assumes the value 1 for all support vectors of the first class and -1 for all support vectors of the seconds class. 
- having performed this transformation step the equation of the two class decision problem can be stated as:

$$
\begin{array}{lccr}
f(x_i) &= x_i \cdot w + b \ge +1, & \textsf{if} & y_i = 1 & \textsf{(for all vectors of class 1)} \\
f(x_i) &= x_i \cdot w + b \le -1, & \textsf{if} & y_i = -1 & \textsf{(for all vectors of class -1)}
\end{array}
$$

The distance between two marginal hyperplanes (**margin width**) is:

$$
\left\{ \frac{2}{\| w \|} \right\}
$$

And so the problem is to find the optimal $w$ and $b$ that maximize this margin width to reach a high classification accuracy and good generalizability. 

This is an optimization problem. The book follow [Support Vector Machine | Wikipedia](https://en.wikipedia.org/wiki/Support_vector_machine) pretty closely except we say $\vec{w}$ is not necessarily normalized, but a normal vector to the hyperplane. 

$$
\vec{w}^T x -b = 0
$$

We don't want just a plane that splits two classes but the plane with the largest margin width. Being a vector we derive the length with $\| \vec{w} \|$. Because we maximize the margin width, which is the inverse, the goal restated can be to minimize $\| \vec{w}  \|$. 

Then we give the constraints we did above. 

And so 

$$
\begin{array}{lll}
\underset{w,\ b}{\textsf{minimize}} & \frac{1}{2} \| \vec{w} \|^2 \\
\textsf{subject to} & y_i(\vec{w}^T \cdot x_i - b) \ge 1 & \forall i \in \{ 1, \dots, n \}
\end{array}
$$

Wiki states most texts will add the intercept. If the value of $y_i f(x_i)$, the y value times the hyperplane linear function, is less than 1, then the instance is **mis-classified**. Errors are used to adjust the vector $\vec{w}$ so the value of the length is minimized but the constraint is fulfilled. 

The algorithm continues to calculate the value of $y_i f(x_i)$ and adjusting the weight vector until all instances are classified correctly and the maximum margin is reached. 

> Like a guess and check!

In the event a hyperplane cannot be found to satisfy the constraints, that's too bad. It pre-supposes that all training instances are on the correct side of the hyperplane. This case is not often feasible in real-life data. Probably because you can only measure a subset of the features that are actually used for classification. 

### 4.2.2 - Nonlinearly Separable Problems (Soft Margin/Primal Form)

We can extend the hard margin formula to consider data instances that lie on the wrong side of the margin. We call this adjusted form of the hard margin the **Primal Form** or **Soft Margin**. 

The constraint of the optimization problem in the case of soft margin is:

$$
\begin{align}
y_i ( x_i \cdot w + b) &\ge +1 \\
1- y_i ( x_i \cdot w + b) &\le 0
\end{align}
$$

constraint are on the previous function of $y_i(\vec{w}^T \cdot x_i + b)$. They could be $-b$ depending on your source. This provides an instance $i$ to violate the separation constraint by a slack error $\xi_i$. 

It might look more like:

$$
1- y_i ( x_i \cdot w + b) \le \xi_i
$$

The error is considered the loss function of having instances on the wrong side of the hyperplane. It can be formulated as follows to consider all intances on the correct and on the wrong side:

$$
\xi_i = \max{\left( 0, 1-y_i \cdot (x_i \cdot \vec{w} _b) \right)}
\tag{4}
$$

For every instance $i$ on the correct side, then $\xi_i = 0$. 

And for each instance on the wrong side, it equals the formula, which is proportional to the distance of this incorrectly classified instance from the marginal hyperplane. 

The **Primal Form** is the constraint optimization problem for detecting a soft-margin. The terms primal and dual are taken from the nomenclature used in Lagrangian Optimization. 

Optimization problem of the hard margin can be relaxed to state the primal form of the soft margin:


$$
\begin{array}{lll}
\underset{w,\ b, \ \xi}{\textsf{minimize}} & \| \vec{w} \|^2_2 + C \sum_{i=1}^n \xi_i\\
\textsf{subject to} & y_i(\vec{w}^T \cdot x_i - b) \ge 1 - \xi_i, & \xi_i \ge 0 & \forall i \in \{ 1, \dots, n \}
\end{array}
\tag{5}
$$

The course book has $C/n$ but Wiki does not. I almost trust Wiki more. 

The $n$ represents the number of instances in the training data of the problem. The regularization parameter $C$ is a problem-dependent parameter. Its value refers to penalty strength of having mis-classifications. Parameter $C$ is considered as a trade-off between:
- If $C$ is small
	- then the classifier can decrease or ignore the penalty of misclassified instances. 
	- In this case, the classifier considers that the data are linearly separable, and the separating hyperplane is smooth and of a hard margin.
- If $C$ is large
	- then the classifier does not allow misclassification where the penalty strength increases. 
	- in this case, the margin is enlarged to form a soft margin that is appropriate for nonlinearly separable data. 
		- this is because the closer points get more weight and this results in the decision boundary which then takes on a piecewise linear form. 

Based on the input dat afor small values of the $C$ parameter, the classification accuracy decreases as more error is allowed. Makes sense.

For larger values of the $C$ parameter, the classification accuracy increases due to overfitting of the training data.

### 4.2.3 - Transformation to Linearly Separable Data

- The SVM linear classifier struggles with nonlinearly separable data.  
- Real-life datasets typically do not allow for constructing a separating hyperplane.  
- A solution involves transforming nonlinearly separable data into a linearly separable form by increasing dimensions in the feature space.  
- This transformation leads to a higher-dimensional feature space from the original.  
- An example illustrates that a circular decision boundary can separate instances of two classes, unlike a straight line (hyperplane).  
- A new dimension (Z) is introduced to the original two-dimensional feature vector (X, Y), creating a three-dimensional space.  
- The added dimension represents the radius of the circular boundary, facilitating linear separability along the z-axis.

The data in an example are separable by the following plane:

$$
Z = X^2 + Y^2 
\tag{6}
$$

This is a circle. 

The transformation process performs an explicit mapping from an $n$-dimensional feature space to a higher $m$-dimensional feature space $(m >> n)$. 

While solving the problem of linearly separable data, this principle suffers from two main problems. 
- Overfitting is the first problem that is caused by the curse of dimensionality. 
- The second problem is the high cost in terms of the computational power needed due to the large size of the transformed feature vectors.

### 4.2.4 - Nonlinearly Separable Problems (Soft Margin/Dual Form)

- Nonlinearly separable problems in SVM utilize the **kernel trick** to avoid explicit transformation of the feature space.  
- This approach reduces computational costs.  
- The SVM algorithm shifts from the primal form of optimization to the **dual form**.  
- The dual form incorporates a Lagrangian multiplier (α) to define the weight vector.

$$
w = \sum_{j = 1}^n \alpha_j y_j x_j
\tag{7}
$$

This defined weight is used in the loss function calculation (4) to obtain the dual form as follows (this is also in the Wiki):

Subject to specific linear constraints, the problem is to find a multiplier $\alpha$ that maximizes the value of the quadratic function $Q$. 

$$
\tag{8}
Q(\alpha)
$$

$$
\begin{array}{ll}
\textsf{maximize} & Q(\alpha) = \sum_{i=1}^n{(\alpha_i)} - \frac{1}{2} \sum_{i=1}^n{\left( 
\sum_{j=1}^n{\left( y_i \alpha_i (x_i \cdot x_j) y_j \alpha_j \right)}
\right)} \\
\textsf{subject to} & \sum_{i=1}^n \alpha_j y_j = 0
\end{array}
$$
  
for all $i, \ 0 \le \alpha_j \le 1 / 2nC$.

- For nonlinearly separable data
	- the original feature space $x_i$ is replaced by another feature space.
		- $\varphi(x_i)$ 
	- Mapping function $\varphi$ performs an explicit transformation of the feature space of an instance $x_i$ to higher dimension feature space $\varphi(x_i)$. 
	- The dot product $x_i \cdot x_j$ in the dual form of the optimization problem is therefore replaced by $\varphi(x_i) \cdot \varphi(x_j)$. 
	- Fortunately
		- the dot product between pairs of mapped data vectors, varphis above, has the same value as the Kernel Function $K$ of the original (non-mapped) feature space of these vectors $x_i$ and $x_j$. 

Mathematical definition of the kernel function:

$$
K(x_i, x_j) = \varphi(x_i) \cdot \varphi(x_j) 
\tag{9}
$$

The Kernel function:
- measures the dot product of the two data vectors X of i and j. 
- can be used as an indicator of the similarity between pairs of data vectors, X of i and j. 
	- in the sense that the distance between two data vectors is inversely proportional to the similarity between these vectors. 

The SVM Kernel Trick is the replacement of every dot product by a nonlinear kernel function. The replacement avoid the explicit transformation of the feature space to a higher dimensional feature space. This is because the kernel function is applied to the original feature space instance without transformation. 

For linearly separable data the mapping function varphi does not change the dimension of the input vector. So you basically have:

$$
K(x_i, x_j) = x_i \cdot x_j 
\tag{10}
$$

- In nonlinearly separable data problems, kernel functions are calculated in the original feature space.  
- The dot product in vector pairs is replaced by a non-linear kernel function.  
- Common types of non-linear kernel functions include polynomial, radial basis function (RBF), and sigmoid kernels.  
- The choice of kernel function depends on the characteristics of the input data.  
- The polynomial kernel represents curved lines, while the radial kernel facilitates closed curves, such as circles or polygons, in the input space.

Common forms of the kernel function on pages 99-100. 
- Polynomial Kernel
- Gaussian Kernel
- Exponential Kernel
- Laplacian Kernel
- Sigmoid Kernel

The proliferation of kernel functions in SVMs exists because **different kernels encode different assumptions about the relationship between features and the decision boundary**.

Here's why we need this variety:

**The fundamental problem**: SVMs work by finding a linear separator, but most real-world data isn't linearly separable. The kernel trick lets us implicitly map data to higher dimensions where it becomes linearly separable, without actually computing those high-dimensional coordinates.

**Why multiple kernels matter**:

Different data has different underlying structures. A polynomial kernel assumes the relationship between features follows polynomial patterns. An RBF (Gaussian) kernel assumes local similarity matters most—points close together should have similar labels. A sigmoid kernel mimics neural network decision boundaries. Each makes different geometric assumptions about how your data clusters.

The "right" kernel depends on your domain. In bioinformatics, string kernels work well for DNA sequences because they capture subsequence similarity. In computer vision, certain kernels exploit spatial relationships in images. For text classification, kernels that measure semantic similarity between documents perform better than generic options.

There's also computational trade-offs. Linear kernels are fastest but least flexible. RBF kernels are powerful but computationally expensive. Polynomial kernels offer middle ground but require tuning the degree parameter carefully.

**Practical perspective**: You typically start with RBF (it's the "Swiss Army knife" kernel—works decently for many problems) and experiment from there based on cross-validation performance. The variety exists because no single kernel dominates across all problem types, and researchers keep designing new ones for specific domains where standard kernels underperform.

For your ML coursework, you'll probably focus on understanding the common ones (linear, polynomial, RBF, sigmoid) and how their parameters affect the decision boundary shape—that intuition transfers when you encounter specialized kernels later.

I'll break down each kernel for you in a practical way.

## The Kernels Explained

**Polynomial Kernel**: K(x, y) = (x·y + c)^d

This captures interactions between features. If you're predicting house prices and suspect that (square_footage × num_bedrooms) matters, polynomial kernels can find these multiplicative relationships.

_Pros_: Good when feature interactions matter, computationally reasonable, interpretable degree parameter _Cons_: Can overfit with high degrees, parameters (d and c) need careful tuning, doesn't handle noise well _When to use_: Image processing, problems where you know features combine multiplicatively, when you have clean data

**Gaussian/RBF Kernel**: K(x, y) = exp(-γ||x - y||²)

_Note_: RBF (Radial Basis Function) and Gaussian are the same thing—RBF is just the general family name. This is the "local similarity" kernel I mentioned earlier.

This creates circular decision boundaries. Points close together in feature space get high similarity scores, distant points get low scores. The γ parameter controls how quickly similarity drops off with distance.

_Pros_: Very flexible, handles non-linear data well, only one main parameter (γ), works great when you have no prior knowledge _Cons_: Can overfit easily, computationally expensive for large datasets, requires good parameter tuning _When to use_: Your default choice, works for most problems, especially when relationships are complex and unknown

**Exponential Kernel**: K(x, y) = exp(-γ||x - y||)

This is like RBF but uses distance instead of squared distance. It decays more slowly, so points further apart still maintain some similarity.

_Pros_: Less sensitive to outliers than RBF, smoother decision boundaries _Cons_: Less commonly used (less community knowledge), can be too smooth for sharp class boundaries _When to use_: When you have noisy data with outliers, when you want gentler transitions between classes

**Laplacian Kernel**: K(x, y) = exp(-γ||x - y||₁)

Uses L1 distance (sum of absolute differences) instead of L2. More robust to outliers in individual dimensions.

_Pros_: Robust to outliers, works well in high dimensions, good for sparse data _Cons_: Less smooth than RBF, harder to tune _When to use_: Text classification, high-dimensional sparse data, when you have outliers in specific features

**Sigmoid Kernel**: K(x, y) = tanh(α·x·y + c)

Mimics neural network activation functions. Creates S-shaped decision boundaries.

_Pros_: Can approximate neural networks, good for certain two-class problems _Cons_: Not always positive semi-definite (can break SVM theory!), limited use cases, tricky parameters _When to use_: Honestly? Rarely. Mostly historical interest or when you specifically want neural network-like behavior

## Simple Kernel Trick Example

Let me show you the **linear kernel** (the simplest case) to illustrate the concept:

**Problem**: Classify points as red or blue. In 1D, we have:

- Red points: x = 1, 2
- Blue point: x = 1.5

In 1D, these aren't linearly separable (the blue point is between the red points).

**The Trick**: Map to 2D using φ(x) = [x, x²]

Now our points become:

- Red: [1, 1] and [2, 4]
- Blue: [1.5, 2.25]

In this 2D space, we can draw a line separating them! The kernel computes K(x, y) = φ(x)·φ(y) = xy + x²y² **without ever explicitly calculating** φ(x) or φ(y).

For x=1, y=2: K(1,2) = 1·2 + 1²·2² = 2 + 4 = 6

This equals [1,1]·[2,4] = 6, but we never actually created those 2D vectors. That's the "trick"—the computational savings become massive in high dimensions.

---

**Quick decision guide for your assignments**:

- Don't know what to use? → **RBF/Gaussian**
- Feature interactions matter? → **Polynomial**
- Noisy/outlier data? → **Laplacian** or **Exponential**
- Avoid sigmoid unless specifically asked

Does this clarify things? Given you're working on claim verification systems, you'll probably find RBF and polynomial kernels most useful for your thesis work.

Great question—this gets at a common misconception about the kernel trick!

**Neither, actually.** We're not creating new points or recalculating vectors. Here's what's really happening:

## What the Kernel Function Does

The kernel function **computes the dot product between two points in the high-dimensional space WITHOUT ever actually transforming the points**.

In my example:

- Original space: x = 1, y = 2 (just numbers)
- Transformed space: φ(x) = [1, 1], φ(y) = [2, 4] (vectors)

**What we DON'T do**: Transform every point with φ(x), store all those high-dimensional vectors, then compute dot products. That would be expensive.

**What we DO**: Use K(x, y) to directly calculate what φ(x)·φ(y) would be, without ever creating φ(x) or φ(y).

## How This Works in Practice

When training an SVM:

1. You keep your original data points (x₁, x₂, ..., xₙ) in their original form
2. When the SVM algorithm needs to compute similarity between point i and point j, it calls K(xᵢ, xⱼ)
3. The kernel returns a single number—the dot product in the transformed space
4. The SVM uses these numbers to find the decision boundary

**You never store transformed versions of your data.** You only compute kernel values on-demand when comparing pairs of points.

## Concrete Example

Training data: x₁=1, x₂=1.5, x₃=2

During SVM training, the algorithm needs to compare points:

- K(x₁, x₂) = 1·1.5 + 1²·1.5² = 1.5 + 2.25 = 3.75
- K(x₁, x₃) = 1·2 + 1²·2² = 2 + 4 = 6
- K(x₂, x₃) = 1.5·2 + 1.5²·2² = 3 + 9 = 12

These three numbers capture the relationships in the transformed space, but we never actually created the points [1,1], [1.5, 2.25], or [2,4].

## Why This Matters

Imagine mapping to a **million-dimensional space** (which some kernels implicitly do!):

- **Bad way**: Transform each point into a million-dimensional vector, store them, compute dot products → memory explosion
- **Kernel trick**: Just compute K(x,y) which might be a simple formula like exp(-γ||x-y||²) → fast and memory-efficient

**The "trick" is that we get all the benefits of high-dimensional space without the computational cost of actually going there.**

Does that clarify it? The kernel is essentially a shortcut function that tells you "if these points were in this fancy high-dimensional space, their dot product would be this number."

So the hyperplane requires some dot product calculation. The Kernel Trick calculates a higher-dimensional value without needing to actually transform the data into a higher dimension. 
- where ever you see $x_i \cdot x_j$ you just use the $K(x_i, x_j)$ instead. 

**Exactly!** You've got it.

The SVM algorithm is fundamentally built on dot products. When finding the optimal hyperplane, it needs to compute things like:

- Distance from a point to the decision boundary: involves dot products
- Which side of the boundary a point falls on: involves dot products
- The optimization problem itself: formulated using dot products

So the entire algorithm can be expressed in terms of dot products between data points. The kernel trick exploits this by saying:

"Everywhere the algorithm needs xᵢ·xⱼ, we'll substitute K(xᵢ, xⱼ) instead"

And since K(xᵢ, xⱢ) = φ(xᵢ)·φ(xⱼ), we're effectively running the SVM in the transformed space **without ever computing φ(x)**.

## The Key Insight

Linear SVM: w·x + b = 0 (hyperplane in original space)

Kernel SVM: The decision function becomes Σ(αᵢ·yᵢ·K(xᵢ, x)) + b = 0

Notice there's no explicit "w" anymore—it's implicitly defined in the high-dimensional space through those kernel computations. The αᵢ values (Lagrange multipliers from optimization) tell you how much each training point (support vector) contributes to the decision.

You've basically understood the central clever idea of kernel methods. This same trick works for other algorithms too (kernel PCA, kernel ridge regression, etc.)—anywhere the algorithm can be reformulated using only dot products, you can "kernelize" it.

Given your background with test automation and attention to implementation details, you might appreciate that this is also why kernel SVMs can be slower than linear SVMs at prediction time—each prediction requires computing K(x_new, x_support_vector) for every support vector, whereas linear SVMs just do one dot product with w.

## 4.3 - SVM for Regression (SVR)

p. 100; 

- SVR (Support Vector Regression) is the regression variant of the SVM (Support Vector Machine) classifier.  
- Unlike SVM, which generates a hyperplane for class label predictions, SVR predicts numerical output values.  
- It is challenging to find a linear function that accurately computes target values for all instances without error.  
- SVR aims to identify a function that allows some deviation from actual target values (epsilon error).  
- The allowed deviation is capped by a threshold ε, which can be adjusted to manage error levels.  
- The primary goal of SVR is to minimize the model coefficient w, focusing on the acceptable error rather than minimizing squared error.  
- The model employs a constraint that the absolute error must remain below ε, providing tunability for model accuracy.


$$
\tag{16}
\begin{array}{ll}
\textsf{minimize} &  \frac{1}{2} \| w \|^2 \\
\textsf{subject to} & | y_i - f(x_i) | \le \varepsilon \\
& f(x_i) = w_i x_i
\end{array}
$$

where $i = 0, \dots, n$, $w_0 = b$, and $x_0 = 1$. 

To consider the error values that are larger than $\varepsilon$ for the points that lie outside the margins, slack variables are introduced, analogous to the soft margin SVM. The cost $C$ represented by the slack variable $\xi_i$ is imposed only on instances that lie outside the margin $\varepsilon$. 

The SVR regression model uses two slack variables, $\{\xi_i, \xi_i^*\}$. I'm not sure what this statement is meant to say. 

This mutates the constraints as follows:


$$
\tag{17}
\begin{array}{ll}
\textsf{minimize} &  \frac{1}{2} \| w \|^2 + C \sum_{i=1}^n{\left( | \xi_i + \xi_i^* | \right)} \\
\textsf{subject to} & | y_i - f(x_i) | \le \varepsilon \\
& f(x_i) = w_i x_i \\
\textsf{and} & | f(x_i) - y_i | \le \varepsilon + |\xi_i^*| \\
 & f(x_i) = w_i x_i
\end{array}
$$

The **additional cost parameter** $C$ can also be tuned to manage the tolerance to points outside of $\varepsilon$. 
- This parameter is considered as a trade-off parameter between the flatness of the function $f$ and the amount up to which deviations larger than $\varepsilon$ are tolerated. 
- As the value of $C$ decreases, the tolerance for points outside of $\varepsilon$ increases.
- And as the value of $C$ approaches zero, the constraint collapses into the simplified form. 

### 4.3.1 - Case Study: Implementation of SVM in Python

There is a 'trialSVM.csv' file somewhere that contains a title row and 100 data rows. Each row contains 6 columns. The first five columns represent the data of the five-featured-instance, with the features of the instances labelled: $\{a, b, c, d, e\}$. 

The feature values are continuous values in the range from 0 to 100. The last column represents the class label of the corresponding instance {class}. The categorization of the class labels in this problem is binary, either Class 0 or Class 1. The class labels are equally (fairly) distributed, such that half of the input data is labeled as Class 0, and the other half is labeled as Class 1. 

The problem can be solved by the support vector machine algorithm tthat is implemented in Scikit-Learn library for the Python programming language. The steps of applying the SVM algorithm can be summarized:
1. Reading and exploring data
2. Data preprocessing
3. Training phase
4. Testing (or evaluating) phase

#### 4.3.1.1 - Reading and Preprocessing of the Input Data

p. 103;

```python
import pandas as pd
from sklearn.model_selection import train_test_split

trial_data = pd.read_csv("trialSVM.csv")
```

Data pre-processing involves dividing of the data into attributes and labels. the value of the shape property is the number of rows and columns. 

```python
print(trial_data.shape)
x = trial_data.drop('Class', axis=1)
y = trial_data['Class']

# The Preprocessing function that receives the name of the used kernel

def classify(kernel_name):
	"""
	"""
	...
	
# Data are divided into training and testing sets
x_train, x_text, y_train, y_test = train_test_split(
	x, y, test_size = 0.20
)
```

#### 4.3.1.2 - Training of the SVM Learning Model

The function for the training step of the support vector machine has an important parameter, called the **kernel type**. The kernel can be:
- linear
- polynomial,
- Gaussian
- sigmoid

We will use the Scikit-Learn SVM library that contains an `SVC` classifier class. It takes on parameter, the kernel type, and returns a training class to fit the data. 

```python
from sklearn.svm import SVC
if kernelName == 'poly':
	svclalssifier = SVC(kernel='poly', degree=8)
else:
	svclassifier = SVC(kernel=kernelName)
print(kernelName)
svclassifier.fit(x_train, y_train)
```

#### 4.3.1.3 - Testing and Evaluation of the SVM Learning Model

The testing step of the SVM involves the prediction of the class labels of the instances `x_test` in the testing part of the dataset. The predict function returns the predicted class labels `y_pred`. Then the code uses the `accuracy_score()` function in the Scikit-Learn "metrics" library to calculate the classification accuracy of the SVM classifier. 

The function finally returns the accuracy value of the calling statement. 

```python
from sklearn.metrics import accuracy_score

y_pred = svclassifier.predict(x_test)
return accuracy_score(y_test, y_pred)
# so the whole time we are in that classify function?
```

Then we apply the classification using the kernels...

```python
print("Linear Accuracy:", classify('linear')) # 0.875
print("Polynomial Accuracy:", classify('poly')) # 1.0
print("Gaussian Accuracy:", classify('rbf')) # 1.0
print("Sigmoid Accuracy:", classify('sigmoid')) # 0.75
```

The analysis of the results show that the sigmoid kernel presented degraded model outputs because it is suitable for binary classification tasks. The model with Guassian kernel achieved the ideal prediction with an accuracy of 100%, and polynomial kernel misclassified one instance. 


## Summary 

p. 105; 

- A standard SVM classifier requires data categories to be well separated by a hyperplane.  
- Finding the optimal hyperplane position is an optimization problem constrained by a margin.  
- Non-linearly separable data can be classified by increasing dimensions, but this is computationally expensive for large datasets.  
- The SVM algorithm uses the kernel trick to avoid costly transformations, replacing the dot product in transformed feature space with a kernel function.  
- The kernel function type varies based on the input dataset and can include linear, polynomial, Gaussian, or sigmoid functions.  
- The SVR algorithm is the regression variant of SVM, which maps the input domain to real numbers rather than specific classes.  
- SVR generates outputs for training data with a maximum deviation of ε from the target.
