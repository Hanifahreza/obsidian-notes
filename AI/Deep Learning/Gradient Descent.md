- It's an optimization algorithm which can give us the best parameter to minimize a function
- In the context of ML, it's most often used to find the optimal weight $w$ to minimize a loss function $L(y, \hat{y})$
- This is done by updating the weight with the derivative $\frac{\partial L}{\partial w}$
- The complete formula is:
			$w' = w - \alpha \frac{\partial L}{\partial w}$
	- $w'$ is the new updated weight
	- $w$ is the old weight
	- $\alpha$ is the [[Learning Rate]]
	- $\frac{\partial L}{\partial w}$ is the gradient of the loss function $L$ w.r.t weight $w$ 
- There are three main types of gradient descent based on **how they calculate the loss**:
	- ##### Gradient Descent
	   - Include all samples for calculating loss
				   $L = \sum_{i=1}^{K} y_i-\hat{y_i}$
	   - Pros:
		   - Guaranteed convergence
		   - Smooth convergence (straight to the optimal point)
	   - Cons:
		   - This will be slow for a huge data
		   - Memory intensive since all the data must be stored in RAM
	- ##### Stochastic Gradient Descent
	   - Include only one sample for calculating loss
				   $L = y_i-\hat{y_i}$ 
	   - Pros:
		   - Faster convergence
		   - Memory efficient
	    - Cons:
		    - It will not go straight to the optimal point, a lot of zigzags
		    - Not guaranteed to be convergent
	- ##### Mini-Batch Stochastic Gradient Descent
	   - Include N samples from K samples for calculating loss
				   $L = \sum_{i=1}^{N} y_i-\hat{y_i}$  
	   - Pros:
		   - Balance between speed and accuracy of convergence
		   - Can be parallelized by processing multiple batches concurrently
	   - Cons:
		   - Not guaranteed to be convergent
		   - Requires tuning for the best batch size
- We can improve SGD and Mini-batch SGD convergence speed with **momentum** by adding velocity ($v$) and momentum ($\gamma$):
	- Initialize $v = 0$
	- Update $v$ with:
		$v' = \gamma v + (1 - \gamma) \frac{\partial L}{\partial w}$
	- Update $w$ with:
		$w' = w - \alpha v$