## Architecture Designs
![[efficientnet.png]]
- **Input Size**: 224x224
- **Parameters**: 7.8 M - 66 M
- It employs [[MobileNet#MBConv Block|MBConv Block]] from MobileNetV2 for a more efficient [[Convolution Operation|convolution]]
### Scaling Factors
![[efficientnet scaling.png]]
- To create a family of models, EfficientNet uses scaling factors for 
	- **Width**: Highest number of [[Convolution Operation|convolution]] kernels (channels)
	- **Depth**: Total number layers in a network
	- **Resolution**: Input image size
- The author found an **efficient** way to scale up the network based on these three factors to balance between model size and accuracy
- The method to balance this is called **Compound Scaling**
- The base model is referred to as "**EfficientNet-B0**," and variants are created by methods such as:
	- EfficientNet-**B1**
	- EfficientNet-**B2**
	- ...
	- EfficientNet-**B7**
### Compound Scaling
![[compound scaling.png]]
- Assume:
	-  **Width** = $W^\phi$
	- **Depth**: $D^\phi$
	- **Resolution**: $R^\phi$
- These factors are optimized by $\phi$ using [[Hyperparameter Tuning#Random Search|random search]] with constrains:
	- $DW^2R^2 \approx 2$
	- $D \geq 1, W \geq 1, R \geq 1$
- With this, we only need to tune $\phi$ instead of the three factors
- The equation is designed such that the total FLOPS would approximately increase by $2^\phi$
- [Source](https://towardsai.net/p/l/efficientnet%E2%80%8A-%E2%80%8Aan-elegant-powerful-cnn)
## Innovations
- **Efficient Building Blocks:** EfficientNet employs efficient building blocks based on [MobileNet#MBConv Block|MBConv Block]] and compound scaling algorithm
- **Advanced Training Techniques:** EfficientNet benefits from advanced training techniques such as stochastic depth and AutoAugment, which help improve model robustness and generalization.
## Performance
![[efficientnet performance.png]]
- **State-of-the-Art Accuracy:** EfficientNet models consistently achieve state-of-the-art performance on various computer vision tasks, including image classification and object detection.
- **Efficiency:** Despite their high accuracy, EfficientNet models are designed to be highly efficient, making them suitable for on-device and real-time applications.
- **Transfer Learning:** Pre-trained EfficientNet models are widely used for transfer learning in computer vision tasks. Their strong feature extraction capabilities enable fine-tuning for specific applications.
## Limitations
- **Resource Requirements:** Even though EfficientNet is efficient relative to its performance, it may still have resource requirements that are not suitable for extremely resource-constrained devices.
- **Complexity:** Deeper variants of EfficientNet, such as EfficientNet-B7, can be computationally complex and may require substantial resources for training and inference.