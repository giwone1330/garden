---
tags:
  - Course
  - Study
  - DeepLearing
---
## Classification
- predict an output from a limited set of answers.
	- *binary* classification
		- positive class
			- yes
			- true
			- 1
		- negative class
			- no
			- false
			- 0
	- decision boundary
- linear regression can be used with a threshold, but it may only perform well on specific data distributions.
- logistic regression

### Logistic regression
- sigmoid function
	-  logistic function
	- output between 0 and 1
	- $g(z)=\frac{1}{1+e^{-z}}, 0\lt g(z)\lt1$
- model
	- $$f_{\vec{w},b}(\vec{x})=g(\vec{w}\cdot\vec{x}+b)=\frac{1}{1+e^{-(\vec{w}\cdot\vec{x}+b)}}\qquad (z=\vec{w}\cdot\vec{x}+b)$$
- interpretation
	- *probability* that the class is 1
	- $f_{\vec{w},b}(\vec{x})=P(y=1|\vec{x};\vec{w},b)$
		- the probability that $y$ is 1, given input $\vec{x}$, parameters $\vec{w}, b$
		- $P(y=0)+P(y=1)=1$

#### Decision boundary
- $f_{\vec{w},b}(\vec{x})=g(\vec{w}\cdot\vec{x}+b)=\frac{1}{1+e^{-(\vec{w}\cdot\vec{x}+b)}}=P(y=1|\vec{x};\vec{w},b)$
- usually the threshold is 0.5 indicating a 50:50chance state
	- is $f_{\vec{w},b}(\vec{x})\ge0.5$ ?
		- yes: $\hat{y}=1$
		- no: $\hat{y}=0$
	- when is $f_{\vec{w},b}(\vec{x})\ge0.5$ ?
		- $g(z)\ge0.5$
		- $z\ge0$
		- $\vec{w}\cdot\vec{x}+b \ge 0$
- so for $f_{\vec{w},b}(\vec{x})=g(z)=g(\vec{w}\cdot\vec{x}+b)$
	- decision boundary is $z=\vec{w}\cdot\vec{x}+b=0$
- Non-linear decision boundaries
	- $f_{\vec{w},b}(\vec{x})=g(w_1x_1^2+w_2x_2^2+b)$
		- $z=x_1^2+x_2^2-1=0$
		- $x_1^2+x_2^2=1$

#### Cost function for logistic regression
- the squared error cost for logistic regression is *non-convex* with lots of local-minima
- $J(\vec{w},b)=\frac{1}{m}\sum_{i=1}^{m}\frac{1}{2}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})^2$
	- loss : $L(f_{\vec{w},b}(\vec{x}^{(i)}),y^{(i)})=\frac{1}{2}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})^2$
- logistic loss
	- $L(f_{\vec{w},b}(\vec{x}^{(i)}),y^{(i)})=$
		- $-\log(f_{\vec{w},b}(\vec{x}^{(i)})), \quad \text{if } y^{(i)}=1$
		- $-\log(1-f_{\vec{w},b}(\vec{x}^{(i)})), \quad \text{if } y^{(i)}=0$
	- loss is 0 if correct, $\infty$ if incorrect
	- this makes the cost function *convex*, thus can reach a global minimum
- simplified loss
	- $L(f_{\vec{w},b}(\vec{x}^{(i)}),y^{(i)})=-y^{(i)}\log(f_{\vec{w},b}(\vec{x}^{(i)}))-(1-y^{(i)})\log(1-f_{\vec{w},b}(\vec{x}^{(i)}))$
- simplified cost function
	- $J(\vec{w},b)=\frac{1}{m}\sum_{i=1}^{m}L(f_{\vec{w},b}(\vec{x}^{(i)}),y^{(i)})$
	- $J(\vec{w},b)=\frac{1}{m}\sum_{i=1}^{m}[-y^{(i)}\log(f_{\vec{w},b}(\vec{x}^{(i)}))-(1-y^{(i)})\log(1-f_{\vec{w},b}(\vec{x}^{(i)}))]$
	- $J(\vec{w},b)=-\frac{1}{m}\sum_{i=1}^{m}[y^{(i)}\log(f_{\vec{w},b}(\vec{x}^{(i)}))+(1-y^{(i)})\log(1-f_{\vec{w},b}(\vec{x}^{(i)}))]$
		- this is derived from **maximum likelihood estimation**

#### Gradient descent for logistic regression
- model
	- $f_{\vec{w},b}(\vec{x})=\frac{1}{1+e^{-(\vec{w}\cdot\vec{x}+b)}}$
- cost function
	- $J(\vec{w},b)=-\frac{1}{m}\sum_{i=1}^{m}[y^{(i)}\log(f_{\vec{w},b}(\vec{x}^{(i)}))+(1-y^{(i)})\log(1-f_{\vec{w},b}(\vec{x}^{(i)}))]$
- gradient descent
	- repeat (until convergence, with simultaneous update)
		- $w_j = w_j - \alpha \frac{\partial}{\partial{w_j}}J(\vec{w}, b)$
			- $\frac{\partial}{\partial{w_j}}J(\vec{w}, b)=\frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})x_j^{(i)}$
		- $b = b - \alpha \frac{\partial}{\partial{b}}J(\vec{w}, b)$
			- $\frac{\partial}{\partial{b}}J(\vec{w}, b)=\frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})$

### The problem of overfitting
- the trained model should generalize well for the task.
- problems
	- underfit
		- does not fit the training set well
		- *high bias*
			- intuition is that the learning algorithm has a strong preconception, a strong bias, that is not learned through training.
		- the potential causes are
			- lack of learning capability
				- model size, number of parameters, model architecture... etc
			- insufficient training
	- overfit
		- fits the training set extremely well, to the point it does not generalize the data that well.
		- *high variance*
			- intuition is that the learning algorithm tries hard to fit exactly to the training data, so that with just a slightly different training data, the function that the algorithm fits could be totally different
		- the potential causes are
			- redundant learning capability
				- model size, number of parameters, model architecture... etc
			- overdone training
			- too much features per data
			- insufficient training data

#### Addressing overfitting
- collect more training examples
- feature selection
	- select features to include/exclude
	- but, useful features could be lost
- regularization
	- reduce the size of parameters $w_j$
		- by convention, regularize $w_1 \sim w_n$ , not $b$

