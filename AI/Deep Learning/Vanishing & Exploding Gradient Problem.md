#### Vanishing Gradient
- It's a problem where during each epoch of training, the computed gradient becomes smaller and smaller to the point of almost zero
- This can happen in a DNN that have a lot of layers 
- It can also happen to DNN that use sigmoid or tanh as its activation function since their output range is small
- Small gradient will lead to small parameter update which will slow or even make convergence unreachable
#### Exploding Gradient
- It's a problem where during each epoch of training, the computed gradient becomes bigger and bigger to the point of very large
- This can happen in a DNN that have a lot of layers 
- It can also happen to DNN with huge initial parameter or huge learning rate
- Huge gradient will lead to unstable learning that makes convergence hard 
#### Solutions
- Use dropout layer:
	- Randomly deactivate $p$ x number_of_neurons with $0 <= p <= 1$ 
	- Adds noise that can also act as regularization method
	- During inference, all neurons will be activated
- Use ReLU activation function that doesn't have a small output range
- Gradient clipping by scaling down gradient if it's above certain threshold
- Use [[Weight Initialization]] algorithm
- Use [[Learning Rate Scheduling]]
- Use [[Batch Normalization]]