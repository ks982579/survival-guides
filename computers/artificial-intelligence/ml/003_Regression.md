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

# 3. Regression

pp. 67-86

Study Goals:
- What is meant by regression.
- The different types of regression analysis.
- The simple linear regression model.
- The different metrics to evaluate regression models.
- The logistic and quantile regression models.
- The regularization approaches in regression analysis.

## Introduction 

Talks about businesses analyzing what drives profit and performance of a business. 

Questions that applying regression analysis to business data may help to resolve:
- Is there a mathematical tool to define such a relationship between process-oriented business indicators and achieved profit?
- What is each of the business's parameters share in said relationship (how much does each parameter contribute)? 

## 3.1 - Linear and Nonlinear Regression

**Regression** is a statistical method that attempts to determine the strength and character of the relationship between dependent variable(s) and independent variable(s). **Regression** is a supervised learning approach, where the given dataset is labeled (i.e., has one or more target variables). 

The goal of regression analysis is to find an expectation for the relationship between the target variable (i.e., dependent variable) and the existent dependent variables within the dataset. 

**Simple Regression** is the regression analysis of a dataset with a single independent variable. 

**Multiple Regression** is the regression analysis of a dataset with multiple independent variables. 

The relationship between the dependent variable and independent variable(s), which is retrieved through a regression analysis, can be either linear or nonlinear. In linear regression, the relationship is a straight-line equation:

$$
y = a_1 \cdot x_1 + a_2 \cdot x_2 + \ \dots \ + a_n \cdot x_n + b
$$

Check out https://en.wikipedia.org/wiki/Regression_analysis - It has statistical mathematical notation. The *hat* is an estimation of population parameters given a sample. 

Note: we are not in a more expressive matrix format. 

We say $\{ x_1, x_2, \dots, x_n \}$ are the independent variables of the dataset. The $\{ a_1, a_2, \dots, a_n \}$ are the coefficients of these variables. Think of those as the weights of each independent variable, that it shares in the resultant target variable $y$. Finally, let ${b}$ be the constant of bias term.

I don't think this is standard statistical notation. 

You can also have **nonlinear regression**,  where the relationship is a nonlinear equation such as polynomial, exponential, etc...

**Nonlinear Regression** is a form of regression analysis where observational data are modeled by a function which is a nonlinear combination of the model parameters. 

In both cases of either linear or nonlinear regression, the objective is to find the optimum values for the coefficients. This will generally follow 4 steps:
1. model selection
2. model fitting
3. model prediction
4. model evaluation

Model selection involves making choices regarding the shape of the model; is it linear or nonlinear, simple or multiple regression? 

Model fitting is employed then to the given dataset to find the unknown coefficients of the chosen model. 

Then the developed model is applied in the model prediction step to estimate the target variable for some other hitherto unseen dataset elements. 

Finally, the inferred model is evaluated in the model evaluation step by checking how close the mode's predictions are to the desired target values.

### 3.1.1 - Simple Linear Regression

Consider we are given one independent variable ($x$) and one *dependent* variable ($y$). We have:

$$
\begin{align}
y &= a \cdot x + b \\
\hat{y} &= y + \varepsilon
\end{align}
$$

Let $\varepsilon$ be the error term such that, I think, $\hat{y} - y = \varepsilon$. The goal is to minimize the error term. We do this by finding values for $a$ and $b$ such that the error term $\varepsilon$ is minimized. 

For each data point, the difference between the predicted value $y$ and the actual observation $\hat{y}$ is the **residue** $\varepsilon$. 

The **Residue** is the difference between the actual and calculated values, also known as the error term of regression. 

The evaluation metric for the simple regression model is the sum of the squared residues, which we aim to minimize. 

$$
\begin{align}
E &= \sum{ \left( \hat{y} - y \right)^2} \\
&= \sum{ \left( \hat{y} - (a \cdot x + b) \right)^2}
\end{align}
$$

From differential calculus, the minimum value of E is derived by setting:

$$
\begin{matrix}
\frac{\partial E}{\partial a} = 0 & \text{and} & \frac{\partial E}{\partial b} = 0
\end{matrix}
$$

We then proceed to solve with optimum settings for both $a$ and $b$ as follows:

$$
\begin{align}
0 &= \frac{\partial E}{\partial b} \\
&= 2 \sum{(\hat{y} - (b + a \cdot x)) \cdot (-1)} \\
&= \sum{\hat{y} - nb -a \sum{x}} \\
&\therefore b = \frac{1}{n} \sum(\hat{y}) - \frac{a}{n} \sum{x}
\end{align}
$$

And similarly

$$
\begin{align}
0 &= \frac{\partial E}{\partial a} \\
&= 2 \sum{(\hat{y} - (b + a \cdot x)) \cdot (-x)} \\
&= -\sum{\hat{y} \cdot x} + b \sum{x} + a \sum{x^2} \\
&= -\sum{\hat{y}x} + \left( \frac{1}{n} \sum{\hat{y} - \frac{a}{n}\sum{x}} \right) \sum{x} + a \sum{x^2} \\
&= a \left( \frac{-1}{n} (\sum{x})^2 + \sum{x^2} \right) - \sum{\hat{y}x} + \frac{1}{n} \sum{\hat{y}} \sum{x} \\
&\therefore a = \frac{n \sum{\hat{y}x} - \sum{\hat{y}} \sum{x}}{ n \sum{x^2} - (\sum{x})^2}
\end{align}
$$

For datasets with more than one independent variable, the same procedure needs to be followed for each of the independent variables to find all the involved parameters. 

### 3.1.2 - R^2 Metric for Correlation Analysis

p. 70;

The **Coefficient of Determination**, in statistics, is a measure of the strength of the relationship between two variables. It is usually squared and called $R^2$. It is *routinely* employed to gauge the quality of fit of the derived regression relationship. 

R-Squared describes the proportion of variance in the dependent variable that is explained by the independent variable. This value ranges from zero to one, where a value close to one indicates a good quality of fit of the regression model. 

https://en.wikipedia.org/wiki/Coefficient_of_determination

Look here if you would like an actual formula.

### 3.1.3 - Test of Linearity

p. 71;

For a developed model to satisfy the linearity assumption, it should pass the test of linearity. The resultant $\varepsilon$ values should be small with respect to a specified threshold. Their values should not follow a significant pattern for the distribution of values. Else, the test for linearity fails and a nonlinear regression model has to be developed for better representation of the dataset. 

It's advised to start with nonlinear or polynomial regression to correlate the data variables in a curvilinear model. 

## 3.2 - Logistic Regression

p. 71;

Linear regression assumes a continuous dependent variable with additive noise that follows a normal distribution with **constant variance**. Conditions are obviously not always met. 

In particular, the dependent variable may follow a binomial distribution and take on categorical values. By this, we mean something like yes/no relates to discrete values 0/1. 

**Logistic Regression** uses a logistic function to model a binary dependent variable. Logistic regression is considered an extension of the linear regression analysis, and its corresponding model can be used to classify input data records into a set of given categories or discrete values that form the dependent variable. 

Example given on page 71 of loan prediction with approved/rejected dependent variable $y$. 

In the example, a linear regression model could present unbounded values for $y$ such that $y = ] -\infty, + \infty [$. Therefore, a logic function $S$ shape is introduced to the linear regression equation and the underlying linear model will map the predictions with the logistic function to produce binary values $\{0, 1\}$. 

Rationale for logistic regression is based on odds ratio. Odds of a specific event occurring are defined as the probability of an event occurring divided by the probability of that even not occurring:

$$
\text{Odds ratio of "1"} = \frac{\text{probability(y=1)}}{1-\text{probability}(y=1)}
$$

The maximum likelihood method generates the logit function that predicts the natural logarithm of the odds ratio:

$$
\log\left( \frac{p}{1-p} \right) = a \cdot x + b
$$

The predicted odds ratio and predicted probability of success are next, giving logistic regression equation:

$$
p(y) = \left( 1 + e^{-(a \cdot x + b)} \right)^{-1}
$$

There's a nice graph on page 73.

## 3.3 - Quantile Regression

In classical linear regression models, the model coefficients are constant across all data records. Coefficients are obtained by minimizing the sum of squares of the residuals. This implies that the *average* changes in the dependent variable across the interval spanned by the values of the independent variable(s) control the resulting model. 

Such a rough assumption is not always true for all datasets. Cases it is not true:
- Skewed data
- Multimodal data
- data with outliers

In the above cases, focus on the average changes in the dependent variable fails to fully capture the structure of the underlying data. 

Therefore, a good approach is to divide the dependent variable into segments (i.e., quantiles) from its lowest value to its highest value and develop a linear regression model for each quantile, known as **Quantile Regression**. 

**Quantile Regression** is an extension of linear regression used when the conditions of linear regression are not met. 

The regression coefficients that define an independent variable's influence on any of the quantiles with respect to their dependent variable are calculated. 

The quantile regression model is developed differently but the interpretation is basically the same as linear regression analysis. 

For Quantile regression, instead of minimizing the sum of the squares of the residuals (E), the objective in quantile regression is to minimize a "weighted" sum of the absolute errors at each quantile of the dependent variable. 

$$
\min\left( \tau \sum_{\text{A}}{| \hat{y} - y |} + (1 - \tau) \cdot \sum_{\text{B}}{| \hat{y} - y |} \right)
$$

Where I am letting $A$ represent the "segments above $\tau$" and letting $B$ represent "segments below $\tau$". Also, $\tau$ represents the quantile level. 

The dependent variables can be divided into a set of quantile levels such as 
$\{5\%, 10\%, 50\%, 90\%, 95\%\}$. By optimizing this loss function, the regression coefficients ($a$ and $b$) are estimated, resulting in a linear relationship between $y$ and $x$ at this specific $\tau$.

The book, page 74, discusses an example of infants' birth weight (dependent variable) and a set of independent variables such as: infant's gender, mother's marital status, existence of pregnancy care, and mother's smoking status. 

Something about how a linear regression model can convey whether a particular independent variable is important for the relationship between independent and dependent variables, it cannot indicate whether a particular independent variable varies according to low or high birth weights. 

Then we do the quantile regression with the percentages mentioned above and get coefficients at each tau. 

The results, both numerical and visual (graphs) show how independent variables have different weights for each quantile and indicate that a *basic* linear regression with average weight for each independent variable might not be an optimal solution to assess the correct mapping to the dependent variable. 

In my experience, this could indicate we need to transform the data to find the linear relationships. 

## 3.4 - Regularization in Regression Analysis

p. 75;

Regression analysis tries to develop the best fit between the independent variables and the dependent variables such that the loss function is minimized and/or the value of $R^2$ is maximized. 

However, the developed model can overfit the training dataset and lose the value of generalization when applied to a different testing dataset. 

Also, while tuning the model for its best fit, the existence of any wrong data points (i.e., outliers) affect the development, leading to an incorrect regression model. 

To avoid issues of overfitting and outliers (i.e., to have a more *robust* model), we penalize the loss function by adding a penalty term to the regression model. 

Such a *penalty* is known as **regularization**. For the case of regression, it comes in two common forms:
- ridge regularization
- lasso regularization

### 3.4.1 - Ridge Regression

Ridge regression is also called $L_2$ Regularization, and proceeds by adding a term to the loss function that penalizes the sum of squares of the model coefficients:

$$
E = \sum{ ( \hat{y} - y )^2} + \lambda \sum{W^2}
$$

where lambda is the constant that controls the level of the penalty, and $W$ stands for the model coefficients. The higher lambda is, the greater its value, the greater the emphasis on the reduction of the coefficients magnitudes. This is at the expense of tolerating higher residuals. 

### 3.4.2 - Lasso Regression

Because of the squared factor, Ridge regression punishes the largest coefficients because their influences are increased when squaring values. Lasso regression, aka $L_1$ regularization, aims to minimize the sum of the absolute values of the coefficients instead of their squares. 

$$
E = \sum{ ( \hat{y} - y )^2} + \lambda \sum{|W|}
$$

Although similar to Ridge regression, the results can vary greatly. Lasso regression preferentially sets some model coefficients to exactly zero, thus favouring sparse models where possible. 

Selecting the optimum value of the regularization parameter lambda is a trade-off. By investigating the model performance over a range of lambda, we get a graph of which value could act better to avoid any unwelcomed overfitting issues. 

## 3.5 - Regression Analysis in Python

We can implement in Python with Scikit-Learn. 

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn import linear_model

plt.style.use('ggplot')

# load dataset
boston_data = datasets.load_boston()
yb = boston_data.target.reshape(-1, 1)
xb = boston_data['data'][:,5].reshape(-1,1)

# Plot the variables
plt.scatter(xb, yb)
p.t.ylabel('value of house /1000 ($)')
plt.xlabel('number of rooms')
plt.show()
```

You should get a lovely graph. Then, continuing on:

```python
# Create model
regr = linear_model.LinearRegression()

# Train the model
regr.fit(xb, yb)

# Generate Plots
plt.scatter(xb, yb, color='black')
plt.plot(xb, regr.predict(xb), color='blue', linewidth=3)
plt.show()
```

You should see perhaps some outliers but the line straight through most data.

Now, a second implementation, with logistic regression model to be developed in Python for a random dataset of binary output {0,1}:

```python
# Dataset
x1 = np.random.normal(size=150)
y1 = (x1 > 0).astype(np.float)
x1[x1 > 0] *= 4
x1 += .3 * np.random.normal(size=150)
x1 = x1.reshape(-1, 1)

# Plotting data
plt.scatter(x1, y1)
plt.ylabel('y1')
plt.xlabel('x1')
plt.show()
```

You should see a plot. Now, more coding:

```python
# run logistic regression analysis
lm_log = linear_model.LogisticRegression()
lm_log.fit(x1, y1)

# Plot model
x1_ordered = np.sort(x1, axis=0)
plt.scatter(x1.ravel(), y1, color='black', zorder=20, alpha = 0.5)
plt.plot(x1_ordered, lm_log.predict_proba(x1_ordered)[:,1], color='blue', linewidth = 3)
plt.ylabel('target variable')
plt.xlabel('predictor variable')
plt.show()
```

The third implementation is Quantile Regression on a random dataset:

```python
# same import from before, and...
import statsmodel.formula.api as smf

# generate random dataset with 2 variables
df = pd.DataFrame(np.random.normal(0, 1, (100, 2)))
df.columns = ['x', 'y']

# linear regression model (for comparison)
x = df['x']
y = df['y']
fit = np.polyfit(x, y, deg=1)
_x = np.linspace(x.min(), x.max(), num=len(y))

# develop quantile regression model for 6 quantiles
model = smf.quantreg('y ~ x', df)
quantiles = [0.05, 0.1, 0.25, 0.5, 0.75, 0.95]
fits = [model.fit(q=q) for q in quantiles]

# quantile lines
_y_005 = fits[0].params['x'] * _x + fits[0].params["Intercept"]
_y_095 = fits[5].params['x'] * _x + fits[5].params["Intercept"]

# Start and end coordinates of quantile lines
p = np.column_stack((x, y))
a = np.array([_x[0], _y_005[0]]) # first point of 0.05 quantile fit line
b = np.array([_x[-1], _y_005[-1]]) # last point of 0.05 quantile fit line
a_ = np.array([_x[0], _y_095[0]])
b_ = np.array([_x[-1], _y_095[-1]]) 

# Mask for coordinates above 0.95 or below 0.05 quantile lines
mask = lambda p, a, b, a_, b_: (np.cross(p-a, b-a) > 0) | (np.cross(p-a_, b_-a_) < 0)
mask = mask(p, a, b, a_, b_)

# Genearte plots
figure, axes = plt.subplots()
axes.scatter(x[mask], df['y'][mask], facecolor='r', edgecolor='none', alpha=0.3, label='data point')
axes.scatter(x[~mask], df['y'][~mask], facecolor='g', edgecolor='none', alpha=0.3, label='data point')
axes.plot(x, fit[0] * x + fit[1], label='best fit', c='lightgrey')
axes.plot(_x, _y_095, label=quantiles[5], c='orange')
axes.plot(_x, _y_005, label=quantiles[0], c='lightblue')
axes.legend()
axes.set_xlabel('x')
axes.set_ylabel('y')
plt.show()
```

And you should get a graph with more lines. We didn't plot all quantiles, just 0.05 and 0.95. 

We do a final implementation with Ridge and Lasso regression using a real dataset again. 

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.model_selection import train_test_split, cross_val_score

from statistics import mean

# Loading the data
data = pd.read_csv('kc_house_data.csv')

# Drop the non-numerical variables and those with missing values
dropColumns = ['id', 'date', 'sqft_above', 'zipcode']
data = data.drop(dropColumns, axis = 1)

# Determine the dependent and independent variables
y = data['price']
X = data.drop('price', axis = 1)

# Divide the data into training and testing set
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25)

# Develop a Linear Regression model
linearModel = LinearRegression()
linearModel.fit(X_train, y_train)

# Evaluate the Linear Regression model
print(linearModel.score(X_test, y_test))

# Develop Ridge(L2) Regression Model:
# Estimate different values for lamda
alpha = []
cross_val_scores_ridge = []
# Loop to compute the different scores
for i in range(1, 9):
	ridgeModel = Ridge(alpha = i * 0.25)
	ridgeModel.fit(X_train, y_train)
	scores = cross_val_score(ridgeModel, X, y, cv = 10)
	avg_cross_val_score = mean(scores)
	cross_val_scores_ridge.append(avg_cross_val_score)
	alpha.append(i * 0.25)
	
# Loop to print the different scores
for i in range(0, len(alpha)):
	print(str(alpha[i])+' : '+str(cross_val_scores_ridge[i]))
# 0.25 : 0.6909039943128887
# 0.5 : 0.690905755445855
# 0.75 : 0.6909073194564496
# 1.0 : 0.6909086883699769
# 1.25 : 0.6909098641885285
# 1.5 : 0.690910848891299
# 1.75 : 0.690911644434875
# 2.0 : 0.6909122527535538

# the best value of lamda for the data is 2
# Build the Ridge Regression model for the best lamda
ridgeModelChosen = Ridge(alpha = 2)
ridgeModelChosen.fit(X_train, y_train)
# Ridge(alpha=2, copy_X=True, fit_intercept=True, max_iter=None, normalize=False, random_state=None, solver='auto', tol=0.001)

# Evaluate the Ridge Regression model
print(ridgeModelChosen.score(X_test, y_test))
# 0.7151525243289275
```

And a break before Lasso Regression:

```python
# Develop Lasso(L1) Regression Model:
# Estimate different values for lamda
lamda = []
cross_val_scores_lasso = []
# Loop to compute the different scores
for i in range(1, 9):
	lassoModel = Lasso(alpha = i * 0.25, tol = 0.0925)
	lassoModel.fit(X_train, y_train)
	scores = cross_val_score(lassoModel, X, y, cv = 10)
	avg_cross_val_score = mean(scores)
	cross_val_scores_lasso.append(avg_cross_val_score)
	lamda.append(i * 0.25)
# Lasso(alpha=0.25, copy_X=True, fit_intercept=True, max_iter=1000, normalize=False, positive=False, precompute=False, random_state=None, selection='cyclic', tol=0.0925, warm_start=False)
# Lasso(alpha=0.5, copy_X=True, fit_intercept=True, max_iter=1000, normalize=False, positive=False, precompute=False, random_state=None, selection='cyclic', tol=0.0925, warm_start=False)
# ...

# Loop to print the different scores
for i in range(0, len(alpha)):
	print(str(alpha[i])+' : '+str(cross_val_scores_lasso[i]))
# 0.25 : 0.6909020889338366
# 0.5 : 0.6909021436304988
# 0.75 : 0.6909021980337026
# 1.0 : 0.6909022521931557
# 1.25 : 0.6909023060760678
# 1.5 : 0.6909023596857342
# 1.75 : 0.6909024130374362
# 2.0 : 0.6909024661093868

# the best value of lamda for the data is 2
# Build the Lasso Regression model for the best lamda
lassoModelChosen = Lasso(alpha = 2, tol = 0.0925)
lassoModelChosen.fit(X_train, y_train)
# Lasso(alpha=2, copy_X=True, fit_intercept=True, max_iter=1000, normalize=False, positive=False, precompute=False, random_state=None, selection='cyclic', tol=0.0925, warm_start=False)

# Evaluate the Lasso Regression model
print(lassoModelChosen.score(X_test, y_test))
# 0.7151811532899977
```

## Summary

p. 86

This unit detailed different algorithms for performing regression analysis. Algorithms included:
- simple linear regression
- logistic regression
- quantile regression

Also included were some implementation in Python. Suitability of each algorithm for a particular case was elaborated. 

Regularization of regression analysis to solve for the problem of overfitting is also explained through the routinely used regularization techniques: ridge and lasso regression. 
