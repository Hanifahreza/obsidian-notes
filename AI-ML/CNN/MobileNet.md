## Architecture Designs
![[mobilenet.png]]
- **Input Size**: 224x224
- **Parameters**: 3.5 M
### Depthwise Separable Convolution 
![[depth-wise conv.png]]
- MobileNet employs depthwise separable [[Convolution Operation|convolutions]], which split standard convolutions into two separate operations:
	- **Depthwise** convolution:
		- Do convolution to each color channels separately
	- **Pointwise** (Spatial) convolution:
		- Combine the results of depthwise convolution to a single tensor
		- Do convolution to each of its points
- This reduces the number of parameters and computations significantly with depthwise convolution to normal convolution ratio:
- $$\frac{N + Dk^2}{N * Dk^2}$$
	- $N$ is the size of the output
	- $Dk$ is the dimension size of the kernel
- [Source](https://medium.com/@godeep48/an-overview-on-mobilenet-an-efficient-mobile-vision-cnn-f301141db94d)
### MBConv Block
- Remember the [[MobileNet#Depthwise Separable Convolution|depthwise separable convolution]] from MobileNetV1
	![[mbconv1.png]]
- MobiletV2 introduces MBConv which is the inverse of it
	![[mbconv2.png]]
- This is **proven to work better** and is **more memory efficient**
	- Because it can now remove the non-linearities in the narrow layers to have better representation power (???)
### Width Multiplier
- It introduces width multiplier hyperparameter to tune model size
- It scales the number of channels in each layer, making it adaptable for various resource constraints
### Resolution Multiplier
- Resolution multiplier is another hyperparameter that allows input image resizing
- This can adjust the model's size and computational requirements
## Innovations
- By reducing the number of parameters and computations with deptwise separable convolution (**V1**) and Mbconv block (**V2**)
	- It becomes very **lightweight** and **efficient** 
- It provides **excellent performance** on **resource-constrained devices**
- It's **optimized** for **real-time inference** on **mobile devices**, making them suitable for applications like object detection and image classification
- The architecture **minimizes latency**, which is crucial for responsive applications, such as augmented reality and mobile vision
## Performance
- **Object Classification:** MobileNet has demonstrated strong performance in object classification tasks, often achieving accuracy similar to larger models with a fraction of the parameters.
- **Object Detection:** MobileNet-based architectures are commonly used in object detection tasks, such as [[SSD]] and [[YOLO]], due to their speed and accuracy trade-offs.
## Limitations
- **Complex Tasks:** While efficient, MobileNet models may not perform as well as larger architectures on highly complex tasks due to their reduced capacity
- **Trade-off:** Achieving efficiency often involves a trade-off with accuracy, and MobileNet is optimized for efficiency