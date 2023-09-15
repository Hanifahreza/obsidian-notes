- After we get a prediction result from [[Forward Propagation]], we want to optimize the model's weights
- Backpropagation is used to here calculate gradients for [[Gradient Descent]] optimization
- It starts from the output layer and moves backward through the network until the first hidden layer (first weight)
- The chain rule is used to compute gradients layer by layer
- Suppose we have a one-hidden-layered neural network:
    $\begin{align*} & x \text{ - Input features (a vector)} \\ & W^{(1)} \text{ - Weights of the hidden layer} \\ & b^{(1)} \text{ - Bias of the hidden layer} \\ & W^{(2)} \text{ - Weights of the output layer} \\ & b^{(2)} \text{ - Bias of the output layer} \\ & a^{(1)} \text{ - Activations of the hidden layer} \\ & a^{(2)} \text{ - Output of the network} \\ & \hat{y} \text{ - Predicted output} \\ & y \text{ - Actual target} \end{align*}$
- First, we perform [[Forward Propagation]]
	$\begin{align*} & z^{(1)} = W^{(1)}x + b^{(1)} \\ & a^{(1)} = \sigma(z^{(1)}) \text{ (Apply activation function)} \\ & z^{(2)} = W^{(2)}a^{(1)} + b^{(2)} \\ & a^{(2)} = \sigma(z^{(2)}) \text{ (Apply activation function)} \\ & \hat{y} = a^{(2)} \end{align*}$
- Then, we perform backpropagation first in the output layer:
	$\begin{align*} & \delta^{(2)} = \frac{\partial L}{\partial a^{(2)}} \cdot \sigma'(z^{(2)}) \\ & \frac{\partial L}{\partial W^{(2)}} = \delta^{(2)} \cdot a^{(1)T} \\ & \frac{\partial L}{\partial b^{(2)}} = \delta^{(2)} \end{align*}$
 - Then we do it in the hidden layer:
	 $\begin{align*} & \delta^{(1)} = (W^{(2)})^T \cdot \delta^{(2)} \cdot \sigma'(z^{(1)}) \\ & \frac{\partial L}{\partial W^{(1)}} = \delta^{(1)} \cdot x^T \\ & \frac{\partial L}{\partial b^{(1)}} = \delta^{(1)} \end{align*}$
- Finally we update all the parameters: 
	$\begin{align*} & W^{(2)} = W^{(2)} - \alpha \cdot \frac{\partial L}{\partial W^{(2)}} \\ & b^{(2)} = b^{(2)} - \alpha \cdot \frac{\partial L}{\partial b^{(2)}} \\ & W^{(1)} = W^{(1)} - \alpha \cdot \frac{\partial L}{\partial W^{(1)}} \\ & b^{(1)} = b^{(1)} - \alpha \cdot \frac{\partial L}{\partial b^{(1)}} \end{align*}$
