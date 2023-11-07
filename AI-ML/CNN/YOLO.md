![[yolo arch.png]]
- Unlike [[R-CNN]], [[Fast R-CNN]], and [[Faster R-CNN]] which only look at **regions of an image**, 
	- **YOLO** looks at the **complete image** and predicts the bounding boxes with its class probabilities
## Key Concepts
### Single-Shot Object Detection
- YOLO is designed to detect objects in a **single forward pass** through the neural network
- Unlike some previous models that involved multiple passes, YOLO operates in real-time
### Grid-Based Detection
![[yolo bbox.png]]
- YOLO **divides the input image** into a **grid** and assigns each grid cell the responsibility of detecting objects within its boundaries
- We compute the **central point** of each of target object's ground truth box and assign it to a grid
- We assign a vector for each central point like $$[P_c, B_x, B_y, B_w, B_h, C_1, C_2, C_{...}]$$
	- $P_c$ is the **probability** of an **object's central point existing at the grid**
	- $B_x$ and $B_y$ are the **coordinate points** of the **central point**
	- $B_w$ and $B_h$ are the **width** and **height** of the **bounding box**
	- $C_1$, $C_2$, $C_{...}$ are the **probabilities** of each **class** for the bounding box
### Non-Maximum Suppression
![[non-max-supp.png]]
- YOLO will produce some bounding boxes for the same object in its prediction
- We use **Non-Maximum Suppression** to pick the correct bounding box:
	- **Input**: 
		- Bounding box proposals $B$
		- Threshold $N$
	- Initialize empty list $D$
	- Select the proposal with highest probability from $B$
		- Remove it from B
		- Add to $D$
	- Calculate the IOU of the proposal in $D$ with every other proposals in $B$:
		- If IOU > $N$, remove the proposal from $B$
	- Repeat until no more proposal in $B$
	- **Return $D$**
## Innovations
- YOLO introduced the concept of single-shot object detection, making it suitable for real-time applications (SoTA)
- Its grid-based approach allows for the detection of multiple objects in a single pass
- YOLO achieved a balance between speed and accuracy in object detection
## Limitations
- YOLO may struggle with small or closely spaced objects due to the coarse grid-based approach
