## Architecture Design
  - VGGNet is characterized by its straightforward architecture, consisting of:
	  - **16** layers (**VGG16**)
	  ![[vgg16.png]]
	  - **19** layers (**VGG19**)
	  ![[vgg19.png]]
  - The two most common configurations are **VGG16** and **VGG19**, which have **16** and **19** layers, respectively
  - **Input Size**: 224x224
  - **Parameters**: 138 Millions
## Innovations
  - It uses only **3x3 [[Convolution Operation|convolution]] filters** with a fixed stride and **2x2 max-pooling** layers
  - The use of **small [[Convolution Operation|convolution]] filters** makes it able to go deeper than its predecessors
## Performance
  - VGGNet achieved top performance in the **2014 ImageNet** Large Scale Visual Recognition Challenge
## Limitations
  - Huge Parameters
  - Huge model size (533 MB)
  - High computational and memory requirements due to the depth of the network
  - Slow training time
