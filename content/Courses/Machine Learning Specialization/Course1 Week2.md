---
tags:
  - DeepLearing
  - Study
  - Course
---
### Multiple Features
- notations
	- $x_j=j^{th} \text{feature}$
	- $n=\text{number of features}$
	- $\overrightarrow{x}^{(i)}=\text{features of } i^{th} \text{ training example}$
	- $x_j^{(i)}=\text{value of feature } j \text{ in } i^{th} \text{ training example}$
- model
	- previously: $f_{w,b}(x)=wx+b$
	- $f_{w,b}(x)=w_1x_1+w_2x_2+ ... +w_nx_n+b$
		- $\vec{w} = [w_1, w_2, w_3, ... , w_n]$
		- $b$ is a number
		- $\vec{x} = [x_1, x_2, x_3, ... , x_n]$
	- $f_{\vec{w}, b}(\vec{x})=\vec{w}\cdot\vec{x}+b$
		- $\cdot$ : dot product
	- *multiple linear regression*
		- not multivariate regression

### Vectorization
- without vectorization
	- $f_{w,b}(x)=w_1x_1+w_2x_2+ ... +w_nx_n+b$
	- $f_{w,b}(x)=\sum_{j=1}^n+b$
- with vectorization
	- $f_{\vec{w}, b}(\vec{x})=\vec{w}\cdot\vec{x}+b$
	- `f = np.dot(w,x) + b`
- efficient and faster computation
	- utilizes parallel hardware
		- in one time-step, element wise multiplication is computed
		- in the next time-step , sum is calculated
	- scale to large datasets

### Gradient descent for multiple linear regression
- model
	- $f_{\vec{w},b}(\vec{x})=\vec{w}\cdot\vec{x}+b$
- parameters
		- $\vec{w} = [w_1, w_2, w_3, ... , w_n]$
		- $b$ is a number
- cost function
	- $J(\vec{w}, b)$
- gradient descent
	- repeat (until convergence, with simultaneous update)
		- $w_j = w_j - \alpha \frac{\partial}{\partial{w_j}}J(\vec{w}, b)$
			- $w_1 = w_1 -\alpha \frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})x_1^{(i)}$
			- ...
			- $w_n = w_n -\alpha \frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})x_n^{(i)}$
		- $b = b - \alpha \frac{\partial}{\partial{b}}J(\vec{w}, b)$
			- $b = b -\alpha \frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})$

#### Normal equation
- only for linear regression, solve $w, b$ without iterations
- but doesn't generalize to other learning algorithms
- slow when number of features is large

### Feature scaling
- problem: if the range / scale of features are different
	- input feature with *relatively wide* range of possible values lead to *small values & narrow range of weight* values for those features.
	- input feature with *relatively narrow* range of possible values lead to *large values & wide range of weight* values for those features.
	- then the contour plot of the parameters will be narrower (ovals with high eccentricity), which in turn makes it harder for gradient descent to converge.
- rescaling the different features to have comparable range of values speeds up and stabilizes gradient descent


#### Div by maximum
- only applicable to features with positive range of values
- limit the max value to 1
- $x_{scaled}=\frac{x}{x_{max}}$

#### Mean normalization
- make all values range from -1 to +1
- min and max values are located at -1 and +1
- $x_{scaled}=\frac{x-\mu}{x_{max}-x_{min}}$

#### Z-score normalization
- make the distribution fit to standard normal distribution (standard gaussian distribution)
- $x_{scaled}=\frac{x-\mu}{\sigma}$

### Checking gradient descent for convergence
- learning curve
	- a graph that shows the change of cost $J(\vec{w}, b)$ to the number of iterations.
	- in normal circumstances, the cost should not increase
		- inappropriate learning rate
		- incorrect implementation
	- when the cost value doesn't decrease for few iterations
		- gradient descent has converged
- automatic convergence test
	- declare convergence when decrease in cost $J(\vec{w}, b)$ is smaller than a specific value (i.e $10^{-3}$)

### Choosing the learning rate
- check the learning curve to debug your training
- if the movement of cost is volatile or increases, try reducing the learning rate.
- if even at very small learning rates, the cost does not decrease continuously, there might be errors in the code implementation.

### Feature engineering
- using *intuition* to design new features, by *transforming* or *combining* original features
	- $f_{\vec{w},b}(\vec{x})=w_1x_1+w_2x_2+b$
		- $x_1$ : frontage
		- $x_2$ : depth
	- $f_{\vec{w},b}(\vec{x})=w_1x_1+w_2x_2+w_3x_3+b$
		- $x_3=x_1x_2$ : area = frontage x depth

### Polynomial regression
- fit nonlinear function to the data
	- $f_{\vec{w},b}=w_1x+w_2x^2+w_3x^3+b$
	- $f_{\vec{w},b}=w_1x+w_2\sqrt{x}+b$
- note that feature scaling becomes much more important when using polynomial regression
- 