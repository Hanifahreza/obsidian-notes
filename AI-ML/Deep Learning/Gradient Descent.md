- It's an optimization algorithm which can give us the best parameter to minimize a function
- In the context of ML, it's most often used to find the optimal weight $w$ to minimize a loss function $L(y, \hat{y})$
- This is done by updating the weight with the derivative $\frac{\partial L}{\partial w}$
- The complete formula is:
- $$
w' = w - \eta \frac{\partial L}{\partial w}
$$
	- $w'$ is the new updated weight
	- $w$ is the old weight
	- $\eta$ is the learning rate
		- This hyperparameter decides how much steps it takes in the direction of the local minimum
		![[learning rate effect.png]]
	- $\frac{\partial L}{\partial w}$ is the gradient of the loss function $L$ w.r.t weight $w$ 
- The computation of gradient descent can be optimized with [[Optimizers]]
- There are three main types of gradient descent based on **how they calculate the loss**
## Gradient Descent
   - Include all samples for calculating loss
	$$L = \sum_{i=1}^{K} y_i-\hat{y_i}$$
### Pros
   - Guaranteed convergence
   - Smooth convergence (straight to the optimal point)
### Cons
   - This will be slow for a huge data
   - Memory intensive since all the data must be stored in RAM
## Stochastic Gradient Descent (SGD)
![[sgd illus.png]]
- Include only one sample for calculating loss
$$L = y_i-\hat{y_i}$$
### Pros
   - Faster convergence
   - Memory efficient
### Cons
- It will not go straight to the optimal point, a lot of zigzags
- Not guaranteed to be convergent	
## Mini-Batch SGD
![[mini batch ilus.png]]
- Include N samples from K samples for calculating loss 
   $$L = \sum_{i=1}^{N} y_i-\hat{y_i}$$
### Pros
   - Balance between speed and accuracy of convergence
   - More stable convergence
   - Can be parallelized by processing multiple batches concurrently
### Cons
   - Not guaranteed to be convergent
   - Requires tuning for the best batch size