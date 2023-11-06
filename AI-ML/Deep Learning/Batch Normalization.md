## Description
- It's a technique used to improve the **training speed** and **performance** of an NN
- It also helps to **stabilize** the training process
- It operates on a [[Gradient Descent#Mini-Batch Stochastic Gradient Descent|mini-batch]] of data as **its own layer**  
![[batch norm layer.png]]
- This layer normalize (actually [[Preprocessing#^ba3b7c|standardize]]) the inputs and output the standardized input
- It's usually placed before or after an activation layer
## Batch Normalization Layer
![[batchnorm layer inside.png]]
- The layer inputs are the outputs of the neurons in the previous layer
- It standardize each input with the formula:
- $$
  \hat{x}_i = \frac{x_i - \mu}{\sqrt{\sigma^2 + \epsilon}}
$$
	- $x_i$ is the i-th input
	- $\mu$ is the mean of the input mini-batch
	- $\sigma^2$ is the std of the input mini-batch
	-  $\epsilon$ is a small constant to prevent division by zero.
- After normalization, it introduces two learnable parameters, typically denoted as $\gamma$ and $\beta$
- These parameters are used to scale and shift the normalized activations,
	- This allows the network to learn the optimal scale and bias for each feature
  $$
  y_i = \gamma \hat{x}_i + \beta
  $$
  - It also keeps track of the moving average of the mean and variance with
  $$
  \begin{align*} &
  \mu_{mov_i} = \alpha \mu_{mov_{i-1}} + (1-\alpha)\mu_i 
 \\&
  \sigma_{mov_i} = \alpha \sigma_{mov_{i-1}} + (1-\alpha)\sigma_i
  \end{align*}
 $$
- The moving averages will be used during inference
![[batchnorm inference.png]]
## Benefits
![[batchnorm contour.png]]
- By uniforming the scale of the features, it smoothen the contour of the data which:
	- Accelerates the training process by reducing internal covariate shift (the change in the distribution of network activations during training)
	- Acts as a form of regularization
	- Allows for the use of higher learning rates without the risk of divergence.
	- Helps make the network less sensitive to weight initialization
