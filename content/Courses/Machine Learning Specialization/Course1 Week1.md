---
tags:
  - DeepLearing
  - Study
  - Course
---

## Overview

> [!info] What is machine learning?
> Science of getting computers to learn without being explicitly programmed.
> (Arthur Samuel - checkers program)


## Supervised vs Unsupervised Machine Learning

- Machine learning algorithms
	- Supervised learning : course 1,2
		- rapid advancements
		- used most in real-world applications
	- Unsupervised learning : course 3
	- Recommender systems
	- Reinforcement learning

+ practical advice for *applying* learning algorithms


### Supervised Learning
- learn input to output mapping using explicit input-correct output pair
- learn from given "*right answers*"

#### Regression : Housing price prediction
- predict a *number*
- from *infinitely* many possible outputs

#### Classification: Breast cancer detection
- predict *categories/classes*
- from *small number* of possible outputs

### Unsupervised Learning
- find something interesting in *unlabeled* data
- Data only comes with inputs x, but not output labels y.
- Algorithm has to find *structure* in the data

#### Clustering
- Group similar data points together.

#### Dimensionality reduction
- Compress data using numbers.

#### Anomaly detection
- find unusual data points.

### Linear regression with one variable
- house sizes and prices
	- size - price data
	- training set
		- $x$ : input variable feature
		- $y$ : output/target variable
		- $m$ : number of training examples
		- $(x, y)$ : single training example
		- $(x^{i}, y^{i})$ : $i^{th}$ training example

#### Process of supervised learning
1. training set is fed to
2. learning algorithm, which will learn
3. a model $f$ to fit a mapping between x to y
	- given an input feature $x$,
	- the model will output $\hat{y}$ , a prediction of y, or estimated y

#### How to represent $f$ ?
- $f_{w,b} = wx + b$
- $f = wx + b$
- this is the mathematical representation of
	- linear regression with one variable
	- Univariate linear regression

#### Cost function
- $w, b$ in $f_{w,b} = wx + b$
	- parameters
	- coefficients
	- weights
- measures how well the line fits the training data
- Squared error cost function
	- $J(w,b)=\frac{1}{2m}\sum_{i=1}^{m}(\hat{y}^{(i)} - y^{(i)})^2$
	- 1/2 times the average of the squared error
	- squared error cost function is *convex*, meaning it will always have one local minima which is the global minima
- goal is to find $w, b$ which makes $\hat{y}^{(i)}$ close to $y^{(i)}$ for all training examples $(x^{(i)}, y^{(i)})$
	- $\text{minimize}_{w,b} J(w,b)$
- The graphical representation of $J(w, b)$ is a 3D plot between $(w, b)$ and $J(w, b)$
	- This can be visualized as contour lines.

#### recap
- model
	- $f_{w,b} = wx + b$
- parameters
	- $w, b$
- cost function
	- $J(w,b)=\frac{1}{2m}\sum_{i=1}^{m}(\hat{y}^{(i)} - y^{(i)})^2$
- objective
	- $\text{minimize}_{w,b} J(w,b)$

### Gradient descent
- an algorithm to find $argmin_{w, b}J(w, b)$
- outline:
	- start with some $w, b$ (e.g $w=0, b=0$)
	- keep changing $w, b$ to reduce $J(w, b)$
	- Until it settle at or is near a minimum
- implementation
	- repeat until convergence, 
		- $w \gets w-\alpha \frac{\partial}{\partial w}J(w, b)$
			- $\alpha$ : learning rate
			- $\frac{\partial}{\partial w}J(w, b)$ : Derivative
		- $b \gets b-\alpha \frac{\partial}{\partial b}J(w, b)$
	- *simultaneously* update $w$ and $b$ !
		- $tmp\_w \gets w-\alpha \frac{\partial}{\partial w}J(w, b)$
		- $tmp\_b \gets b-\alpha \frac{\partial}{\partial b}J(w, b)$
		- $w=tmp\_w$
		- $b=tmp\_b$
- intuition
	- the partial derivative means the *movement in cost function value* $J(w,b)$, *for the increment in derivating variable*.
	- by multiplying $-\alpha$ , a negative value, $-\alpha \frac{\partial}{\partial w}J(w, b)$ always points to the *direction of the derivating variable*, where the $J(w, b)$ value **decreases**.
- when already at local minima, the parameters are updated to the same value, since the deriative is zero.
- near a local minima,
	- derivative becomes smaller
	- update steps become smaller
	- so gradient descent can reach minimum without decreasing learning rate $\alpha$

#### Learning rate
- if $\alpha$ is too small, gradient descent may be slow.
- if $\alpha$ is too large, gradient descent may overshoot, fail to converge, diverge

### Gradient descent for linear regression
- linear regression model
	- $f_{w,b}(x)=wx+b$
- cost function
	- $J(w,b)=\frac{1}{2m}\sum_{i=1}^{m}(f_{w,b}(x^{(i)})-y^{(i)})^2$
- gradient descent algorithm
	- $w \gets w-\alpha \frac{\partial}{\partial w}J(w, b)$
		- $\frac{\partial}{\partial w}J(w, b) = \frac{1}{m}\sum_{i=1}^{m}(f_{w,b}(x^{(i)})-y^{(i)})x^{(i)}$
		- $w \gets w-\alpha \frac{1}{m}\sum_{i=1}^{m}(f_{w,b}(x^{(i)})-y^{(i)})x^{(i)}$
	- $b \gets b-\alpha \frac{\partial}{\partial b}J(w, b)$
		- $\frac{\partial}{\partial b}J(w, b) = \frac{1}{m}\sum_{i=1}^{m}(f_{w,b}(x^{(i)})-y^{(i)})$
		- $b \gets b-\alpha \frac{1}{m}\sum_{i=1}^{m}(f_{w,b}(x^{(i)})-y^{(i)})$

#### *Batch* gradient descent
- each step of gradient descent uses *all* the training examples