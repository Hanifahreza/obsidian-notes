![[optimizers.gif]]
## Momentum
![[momentum.png]]
- **Momentum** improves SGD and Mini-batch SGD convergence speed by adding velocity ($v$) and momentum hyperparameter ($\gamma$):
	- Initialize $v = 0$
	- Update $v$ with:
	$$v' = \gamma v + (1 - \gamma) \frac{\partial L}{\partial w}$$
	- Update $w$ with:
	$$w' = w - \eta v'$$
	- $\gamma$ usually set to $0.9$ or $0.95$
### Pros
- Momentum helps to reduce noise
- It also smoothen the curve
### Cons
- Extra hyperparameter
## Adaptive Gradient Descent (AdaGrad)
- Use different learning rate for each neuron in each hidden layer based on different iterations
- The learning rate is updated based on the previous learning rate
	- Update the weight
	$$w_t = w_{t-1} - \eta_t \frac{\partial L}{\partial w_{t-1}}$$
	- $\eta_t$ itself is computed using previous learning rate $\eta_{t-1}$
	- $$\eta_t = \frac{\eta_{t-1}}{\sqrt{\alpha_t + \epsilon}}  $$
		- $\alpha_t$ is the sum of all previous gradients squared
		$$\alpha_t = \sum_{i=1}^t (\frac{\partial L}{\partial w_i})^2 $$
		- $\epsilon$ is a small positive number to prevent the denominator becoming 0
	- As the time $t$ progresses, 
		- The denominator will be bigger
		- The learning rate will be smaller
		- Hence, the learning rate is "slowing down" when it's closer to optimal point
### Pros
- Learning rate adapts at each iteration
- It's good for sparse data
### Cons
- if $\alpha$ is too big, it can effectively stop the weight update (training)
## AdaDelta & RMS-Prop
- Sometimes $\alpha_t$ is becoming too huge such that the weight update is very small
- We deal with this by modifying $\alpha_t$ formula to
- $$\alpha_t = \gamma \alpha_{t-1} + (1-\gamma)(\frac{\partial L}{\partial w})^2 $$
	- $\gamma$ is a hyperparameter usually set to $0.9$ or $0.95$
### Pros
- Better than AdaGrad since they addres AdaGrad's issue
### Cons
- Learning is slower
## Adam
- Combine momentum with RMS-Prop:
	- Update $v$ with momentum method:
	- $$v_t = \gamma_1 v_{t-1} + (1 - \gamma_1) \frac{\partial L}{\partial w}$$
		- $\gamma_1$ is a hyperparameter usually set to $0.9$
	- Update learning rate $\eta$ with RMS-Prop:
	- $$ \begin{align*}&
	\eta_t = \frac{\eta_{t-1}}{\sqrt{\alpha_t + \epsilon}} \\&
	\alpha_t = \gamma_2 \alpha_{t-1} + (1-\gamma_2)(\frac{\partial L}{\partial w})^2 
	 \end{align*}$$
		 - $\gamma_2$ is a hyperparameter usually set to $0.999$
	- Update $w$ with:
	$$w_t = w_{t-1} - \eta_t v_t$$
### Pros
- Computationally efficient
- Little memory cost
- It's the SoTA along with AdamW
## AdamW
- Adam, but with [[Regularization#Ridge Regression (L2 Regularization)|weight decay]]
- It differs with Adam in the weight update
- $$w_t = w_{t-1} - \eta_t v_t - \eta_{t}w_{t-1}\lambda$$
	- $\lambda$ is the weight decay hyperparameter
### Pros
- It's the SoTA along with Adam