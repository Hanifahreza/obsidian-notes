- Convolution is actually in mathematics called **Cross-Correlation** 
- It works like the GIF below
![[conv.gif]]
- With the input dimension $n$ x $n$ and kernel dimension $f$ x $f$, the output will have a dimension of $(n-f+1)$ x $(n-f+1)$ 
- However, there are some problems with this operation alone that must be solved with [[Padding]]
- We can also make this operation faster with [[Pooling]]
- The output of these operations will be put into [[Fully Connected Layers]]
- We add [[Activation Function]] to introduce non-linearity after a convolution layer
## Stride
- It's actually not necessary for the kernel sliding window to only move by 1 pixel at a time
- We can configure how many pixels to slide with **Stride**
## Translation Equivariance
- Convolution satisfies **translation equivariance** because it preserves information about the location of input features
- This means, if **translation** is done onto the **input**, the **output** will also **translates the same way**
![[equivariance.png]]
## Benefits
- This operation is used to **identify edges feature** from an image
![[edges_conv.png]]
- A CNN network will use a lot of filters to detect different kind of features from an image
-  In a colored RGB image, the filter will be 3D since there are extra 3 color channels to deal with
![[colored-conv.png]]
- A convolutional layer of a CNN for colored image would look something like this
![[cnn-conv-layer.png]]