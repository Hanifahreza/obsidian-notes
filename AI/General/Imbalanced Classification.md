- It's when the ratio of samples between classes is severe, e.g. 1:100
- This makes it so that during training the minority class is rare to come by and hard to learn
- It’s compounding: 
	- If there are multiple clusters of the minority class that has overlap with the majority class, It’d only look like noise
- Solutions:
	- **Stratification**
	- **Oversampling**
	- **Undersampling**
	- **Combined Techniques**
	- **Cost-Sensitive Learning**
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
### Condensed Nearest Neighbor (CNN) Rule 
### Tomek Links Undersampling
### Edited Nearest Neighbors (ENN) Rule
### One-Sided Selection (OSS)