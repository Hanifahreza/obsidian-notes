- Activation functions are what make a deep learning model not linear
- Its input is an output of a linear function
- They are also differentiable which comes handy for optimization
- Below are the most popular activation functions
#### ReLU
- The simplest of all activation functions
- Formula:
				$f(x) = \max(0, x)$
#### Sigmoid 
- It's a function that map a vector of numbers in range $[-\infty, \infty]$ to a vector of probabilities of the same dimension that adds up to 1
- It's used to translate a result of regression to classification in the form of probability vector
- Say we have a regression result vector $y$ for $N$ classes, the softmax formula is:
								$\text{sigmoid}(\mathbf{y_i}) = \sum_{j=1}^{N}\frac{1}{1+e^{-y_j}}$
#### Softmax
- It's a function that map a vector of numbers in range $[-\infty, \infty]$ to a vector of probabilities of the same dimension that adds up to 1
- It's used to translate a result of regression to classification in the form of probability vector
- Say we have a regression result vector $y$ for $N$ classes, the softmax formula is:
								$\text{softmax}(\mathbf{y_i}) = \frac{e^{y_i}}{\sum_{j=1}^{N} e^{y_j}}$
