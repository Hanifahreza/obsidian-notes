## Vanishing Gradient
- It's a problem where during each epoch of training, the computed gradient becomes smaller and smaller to the point of almost zero
- This can happen in a DNN that have a lot of layers 
- This usually happens when the computed gradients are in range $(0,1)$
- It can also happen to DNN that use sigmoid or tanh as its activation function since their output range is small
- Small gradient will lead to small parameter update which will slow or even make convergence unreachable
## Exploding Gradient
- It's a problem where during each epoch of training, the computed gradient becomes bigger and bigger to the point of very large
- This can happen in a DNN that have a lot of layers 
- This usually happens when the computed gradients are $> 1$
- It can also happen to DNN with huge initial parameter or huge learning rate
- Huge gradient will lead to unstable learning that makes convergence hard 
## Solutions
- Use **dropout layer**:
	- Randomly deactivate $p$ x number_of_neurons with $0 <= p <= 1$ 
	- Adds noise that can also act as regularization method
	- During inference, all neurons will be activated
- Use gradient clipping by cutting the value of gradient $g$ $$g' = g \cdot \min(1, \frac{c}{||g||})$$
- Use non-saturating [[Activation Function]] that doesn't have a small output range
![[non-saturating activ.png]]
- Use [[Weight Initialization]] algorithm
- Use [[Learning Rate Decay]]
- Use [[Batch Normalization]]
- Use [[ResNet#Skip Connections|Residual Connection]]