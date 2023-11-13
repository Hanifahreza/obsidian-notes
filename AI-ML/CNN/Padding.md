- A problem with convolution operation is that the output dimension will always be reduced after the operation
- Another problem is that the outer pixels will always get less attention than the inner pixels
![[why-pad2.png]]
- We can solve this by **padding** the input with outer layers of 0
- This will solve the attention problem
![[why-pad.png]]
- There are two types of convolution w.r.t padding:
	- **Valid Convolution**:  Basically convolution with no padding
	- **Same Convolution**: Making the output size the same as the input size with padding