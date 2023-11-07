![[fast r-cnn.png]]
- Fast R-CNN is an evolution of [[R-CNN]] 
## Key Concepts
### Region of Interest (RoI) Pooling
- Instead of feeding thousands of RoIs to the [[Convolution Operation|CNN]], we feed the input image directly to the CNN
- Let the CNN create a feature map from which we identify the RoIs using [[R-CNN#^25152a|selective search algorithm]] and warp them into squares
- **RoI Pooling Layer** is used to reshape the RoIs into a fixed size to be fed into a [[Fully Connected Layers]]
- Use [[Activation Function#Softmax|Softmax Layer]] to predict the class of the proposed region
### Single Forward Pass
- Unlike the multiple forward passes required in R-CNN, Fast R-CNN performs object detection in a single forward pass through the network
- This results in faster processing
### Unified Framework
- Fast R-CNN unifies the region proposal generation and object detection stages into a single network, making it possible to train the entire system end-to-end
### Shared Convolutional Features
- Fast R-CNN shares convolutional features across all RoIs, reducing redundant computation and improving efficiency
## Limitations
![[fast r-cnn bottleneck.png]]
- While Fast R-CNN is faster and more accurate than R-CNN, it may still not be suitable for real-time applications on resource-constrained devices.
- Training Fast R-CNN models can be computationally intensive due to the need for a **region proposal** that becomes the **bottlenect** of Fast R-CNN
