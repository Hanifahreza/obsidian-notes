## Architecture Designs
- ResNet variation consists of:
	- **ResNet18**: 18 Layers
	  ![[resnet18.png]]
	  - **ResNet50**: 50 Layers
	 ![[resnet50.png]]
- **Input size**: 224x224
- **Parameters**: 
	- ResNet18: 11.7 M
	- ResNet50: 25.6 M
### Skip Connections
![[skip connection.png]]
- ResNet introduces **skip connections**, also known as residual connections
- These connections bypass one or more layers and allow the gradient to flow directly through the network when there's an indication [[Vanishing & Exploding Gradient Problem#Vanishing Gradient|vanishing gradient]]
- They enable the training of extremely deep networks without suffering from the vanishing gradient problem.
![[skip connection app.png]]
- When there's a layer that's not learning and blocking the next layers, we can just skip it with the connection
### Residual Blocks
![[residual block.png]]
- ResNet uses a basic building block called the **residual block**:
	- It consists of two or more [[Convolution Operation|convolutional layers]] with skip connections
	- These blocks are stacked together to form deep networks
### Bottleneck Layers
![[resnet bottleneck.png]]
- Bottleneck layers are introduced to reduce computational complexity like in [[InceptionNet (GoogleNet)]]
- These layers use 1x1 convolutions to reduce the number of channels before applying 3x3 convolutions
## Innovations
- Skip connections address the [[Vanishing & Exploding Gradient Problem#Vanishing Gradient|vanishing gradient]] problem by providing a direct path for gradients to flow backward, enabling the training of very deep networks
## Performance
- **ImageNet Challenge:** ResNet achieved top performance in the ImageNet Large Scale Visual Recognition Challenge. It significantly reduced the top-5 error rate, making it the leading architecture in image classification.
- **Baseline Model**: It has now become the standard when we need to use a relatively simple and light model for CV tasks
## Limitations
- ?