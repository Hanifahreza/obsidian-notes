- We want to separate samples into 2 classes
- We can do this by drawing a 1D line or 2D, 3D, etc hyperplane to separate both classes
- However this is not always possible as demonstrated by the picture below
  ![[svm_use_case.png]]
  - To separate them, we use kernel trick in which we bring the samples to a higher dimension
  - To save computation cost, instead of transforming it directly to higher dimension, we only need to know the dot product in the higher dimension using **kernel function**
  - The output of the kernels are real number that act as the **dot product** of two data points
## Linear kernel
$$K(x_i, x_j) = x_i^T x_j$$
### Pros
- Simple
### Cons
- Can't perform well in non-linear boundary
## Polynomial kernel
- $$K(x_i, x_j) = (\gamma \langle x_i, x_j \rangle + r)^d$$
	- $\gamma$ is the coefficient of the kernel
	- $d$ is the value of the desired higher dimension
	- $r$ is bias
### Pros:
- Can perform well in non-linear boundary
- Moderate computational cost
- Can adjust the degree to balance over and underfitting
### Cons:
- Sensitive to degree hyperparameter
## RBF kernel:
- $$K(x_i, x_j) = \exp(-\gamma * ||x - y||^2))$$
	- $\gamma$ is positive scaling hyperparameter
### Pros:
- Can perform well in non-linear boundary
- Tends to generalize well for unseen data
- Works the best for real life data
### Cons:
- Quite complex and computationally expensive
- Needs hyperparameter tuning, especially for gamma
## Sigmoid kernel:
- $$K(x_i, x_j) = \tanh(\alpha x^Ty + c)$$
	- $\alpha$ is scaling hyperparameter
	- $c$ is a constant hyperparameter
### Pros:
- Can perform well in non-linear boundary
- Suitable for binary classification
### Cons:
- Sensitive to hyperparameters
- Prone to overfitting
