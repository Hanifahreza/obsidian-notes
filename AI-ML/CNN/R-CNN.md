![[R-CNN.png]]
## Workflow
### Region Proposal
- R-CNN uses a **selective search** algorithm to generate **2000 region proposals** from an input image ^25152a
	- Generate initial sub-segmentation, we generate many candidate regions  
	- Use greedy algorithm to recursively combine similar regions into larger ones   
	- Use the generated regions to produce the final candidate region proposals
- These proposals are **regions of interest (ROIs)** that **might contain objects**
- The ROIs are warped into a square and fed into a [[Convolution Operation|CNN]] 
### Feature Extraction
- Use a typical CNN like [[VGGNet]] or [[ResNet]] to extract features of ever ROI 
- These features are used for object classification and bounding box regression
- The CNN will produce a **4096**-dimensional feature vector as output
### Object Classification 
![[r-cnn2.png]]
- A separate [[Support Vector Machine (SVM)|SVM]] is trained for each object category to classify objects within region proposals
- The features extracted from the CNN are used as input to these SVM classifiers
### Bounding Box Regression 
- R-CNN employs **bounding box regression** to refine the region proposals and predict tighter bounding boxes around objects
## Innovations
- R-CNN introduced the concept of **region-based processing** for object detection, 
	- Which was a significant departure from earlier sliding window approaches
- It demonstrated the effectiveness of combining region proposals with deep learning for object detection tasks
## Limitations
- R-CNN can be slow due to the need to extract features for multiple region (2000) proposals, making it less suitable for real-time applications
- The model requires substantial computational resources and training time
- The object classification step with SVMs is a sequential process, which adds to the inference time
- The selective search algorithm is a fixed algorithm with no learning happening
	- This could lead to bad candidate region proposals