- Activation functions are what make a deep learning model not linear
- Its input is an output of a linear function
- They are also differentiable which comes handy for optimization
## ReLU
![[relu.png]]
- The simplest of all activation functions
					![[relu decision.png]]
- It will make **sharp edges and corners** when creating a decision boundary
- Formula:
$$\text{relu}(y) = \max(0, y)$$
## Tanh
![[tanh.png]]
- It's a function that map a vector of numbers in range $[-1, 1]$ to a probability between $0$ and $1$ of belonging to a class
				![[tanh decision.png]]
- It will make **smooth edges and corners** when creating a decision boundary
- The formula is:
$$\text{tanh}(\mathbf{y_i}) = \sum_{j=1}^{N}\frac{e^{y_j}-e^{-y_j}}{e_{y_j} +e^{-y_j}}$$
## Sigmoid 
- It's a function that map a vector of numbers in range $[-\infty, \infty]$ to a probability between $0$ and $1$ of belonging to a class
- It's used to translate a result of regression to classification in the form of probability value (**Binary Classification**)
- Say we have a regression with result vector $y$ for $N$ classes, the sigmoid formula is:
$$\text{sigmoid}(\mathbf{y_i}) = \sum_{j=1}^{N}\frac{1}{1+e^{-y_j}}$$
## Softmax
- It's a function that map a vector of numbers in range $[-\infty, \infty]$ to a vector of probabilities of the same dimension that adds up to 1
- It's used to translate a result of regression to classification in the form of probability vector (**Multi-Class Classification**)
- Say we have a regression result vector $y$ for $N$ classes, the softmax formula is:
$$\text{softmax}(\mathbf{y_i}) = \frac{e^{y_i}}{\sum_{j=1}^{N} e^{y_j}}$$
