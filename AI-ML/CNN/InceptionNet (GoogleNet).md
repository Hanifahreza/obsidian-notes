## Architecture Designs
![[googlenet.png]]
- **Layers**: 22 layers (27 including pooling layers)
- **Input size**: 299x299
- **Parameters**: 6.6 M
### Inception Module
- InceptionNet introduced the concept of an "**Inception module**" which incorporates multiple filters of different sizes in parallel
![[inception module.png]]
- This allows the network to capture features at various scales
- It employs multiple pathways or branches within the network to process the input data
- Each branch uses a different filter size to extract features
### Global Average Pooling
- Instead of [[Fully Connected Layers]] at the end of the network, InceptionNet uses global [[Pooling#Average Pooling|average pooling]]
	- This reduces overfitting and the number of parameters
### Reduction Blocks
![[reduction blocks 1.png|number of operations = (14x14x48)x(5x5x480) = 112.9M]]
![[reduction blocks 2.png|Number of operations = (14x14x48)x(5x5x16) = 3.8M]]
- To reduce the spatial dimensions, 
	- Reduction blocks with 1x1 [[Convolution Operation|convolutions]] are used instead of with higher kernel
	- This helps in reducing computational load
## Innovations
- It demonstrated that by using a large number of smaller filters (e.g., 3x3 and 5x5) in parallel, 
	- The network can **capture complex features efficiently** without an excessive increase in the number of parameters.
- It successfully make a **deeper network** with less cost
- The use of global average pooling and the reduction of fully connected layers **reduced overfitting** and improved generalization.
## Performance
- **ImageNet Challenge:** InceptionNet performed exceptionally well in the 2014 ImageNet Large Scale Visual Recognition Challenge. It significantly reduced the top-5 error rate.
## Limitations
- ?
