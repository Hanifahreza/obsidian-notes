- Forward propagation is the process of making predictions based on the input data
- It's a **feedforward** process, where input data flows in one direction: from **input layer to output layer**
- Suppose we have a one-hidden-layered neural network:

    > $\begin{align*} & x \text{ - Input features (a vector)} \\ & W^{(1)} \text{ - Weights of the hidden layer} \\ & b^{(1)} \text{ - Bias of the hidden layer} \\ & W^{(2)} \text{ - Weights of the output layer} \\ & b^{(2)} \text{ - Bias of the output layer} \\ & a^{(1)} \text{ - Activations of the hidden layer} \\ & a^{(2)} \text{ - Output of the network} \\ & \hat{y} \text{ - Predicted output} \\ & y \text{ - Actual target} \end{align*}$

- We perform forward propagation like this:
  
	> $\begin{align*} & z^{(1)} = W^{(1)}x + b^{(1)} \\ & a^{(1)} = \sigma(z^{(1)}) \text{ (Apply activation function)} \\ & z^{(2)} = W^{(2)}a^{(1)} + b^{(2)} \\ & a^{(2)} = \sigma(z^{(2)}) \text{ (Apply activation function)} \\ & \hat{y} = a^{(2)} \end{align*}$
