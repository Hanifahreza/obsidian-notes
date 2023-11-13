- It's when the ratio of samples between classes is severe, e.g. 1:100
- This makes it so that during training the minority class is rare to come by and hard to learn
- It’s compounding: 
	- If there are multiple clusters of the minority class that has overlap with the majority class, It’d only look like noise
- Solutions:
	- **Stratification**
	- **Oversampling**
	- **Undersampling**
	- **Combined Technique**
	- **Cost-Sensitive Learning**
	- **Weighted Loss**
## Stratification
- It doesn't impact anything to the class distribution
- Its purpose is just to maintain the class distribution when dealing with the data
### Stratified K-Fold
- [[K-Fold Validation]], but try to maintain the class distribution when partitioning
### Stratified Train-Test Split
- Split the data to train and test dataset with the same class distribution as the original data
## Oversampling
- Make new synthetic samples for the minority class
### Random Oversampling
- Randomly duplicate examples in the minority class
- Also works for multi-class classification
- Help skewed distributions for algorithms that
	- Iteratively learn coefficients
		- e.g. NN+[[Gradient Descent#Stochastic Gradient Descent|SGD]]
	- Seek good splits
		- e.g. [[Support Vector Machine (SVM)|SVM]], [[Decision Tree]]
- **Monitor its performance** on **both train and testing** datasets to compare is a good idea
### Synthetic Minority Oversampling Technique (SMOTE)
- Synthesize new samples by:
	- Taking some [[K-Nearest Neighbors (KNN)|KNN]] from a random sample
	- Drawing a line between those samples
	- Creating new samples on that line between the samples
- Sometimes we do random undersampling first to balance the distribution, and then SMOTE to oversample
### Borderline-SMOTE
- Extension of SMOTE where the selected samples are instances in the minority class that are misclassified by [[K-Nearest Neighbors (KNN)|KNN]] 
- Don’t actually make a discriminative model
	- Weight the minority class with density of data
	- Pick the lowest density as focus
### Borderline Oversampling with SVM
- [[Support Vector Machine (SVM)|SVM]] used instead of [[K-Nearest Neighbors (KNN)|KNN]] to identify misclassified examples on the decision boundary
### Adaptive Synthetic Sampling (ADASYN)
- Adaptive generating minority data samples according to the known distributions
- Generate data on the outlier places according to distribution that are hard to learn instead of the ones that are easier to learn
- May create worse model performance when low density examples are outliers
	- i.e. It’s actually over-representing the outliers
## Undersampling
- Remove samples from the majority class
### Random Undersampling
- Randomly delete examples in the majority class
- Same effect as random oversampling
### Near-Miss Undersampling
- Select examples based on the distance of the majority class example to minority class example
#### NearMiss-1
- Majority class examples with min avg distance to 3 closest minority class example
#### NearMiss-2
- Majority class example with min avg distance to 3 farthest minority class example
#### NearMiss-3
- Majority class example with min distance to each minority class example
### Condensed Nearest Neighbor (CNN) Rule 
- Seek subset of samples that result in no loss in model performance
- Also known as minimal consistent set
### Tomek Links Undersampling
- CNN may allow redundant examples due to random selection
- CNN may allow examples that are internal to the mass of the distribution, instead of the boundary
- A Tomek link from $A$ to $B$ is such that:
	- $A$'s nearest neighbor is $B$
	- $B$’s nearest neighbor is $A$
	- $A$ and $B$ belong to different classes
- Or that is to say, a **cross-class nearest neighbor**
- Using this, if the example in the minority class is held constant:
	- We can remove the majority class closest to the minority class
### Edited Nearest Neighbors (ENN) Rule
- Find a sample $x$’s 3 nearest neighbors
- If $x$ is misclassified due to its 3 nearest neighbors:
	- If $x$ is majority class
		- Delete $x$
	- If $x$ is minority class
		- Delete $x$’s 3 neighbors
### One-Sided Selection (OSS)
- Tomek Link + CNN
### Neighborhood Cleaning Rule (NCR)
- CNN + ENN
## Combined Technique
- Pipeline oversampling + undersampling
- Standard methods:
	- SMOTE + Tomek
	- SMOTE + ENN
## Cost Sensitive Learning
- TODO
## Weighted Loss
- Add more weights to samples in minority class during loss function computation