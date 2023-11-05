## External Measures
### Confusion Matrix
![[confusion matrix.png]]
- $\text{Accuracy} = \frac{TP + TN}{\text{Total Population}}$
- $\text{Precision} = \frac{TP}{TP + FP}$
- $\text{Recall} = \frac{TP}{TP + FN}$
- $\text{Specificity} = \frac{TN}{TN + FP}$
- $\text{FPR} = 1 - \text{Specifity} = \frac{FP}{TN + FP}$
- $\text{F1 Score} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$
### ROC - AUC
- It's a curve with $FPR$ as the $x$-axis and $TPR$ as the $y$-axis
- Sometimes $TPR$ can be replaced with precision when the data is imbalanced
![[roc-auc.png]]
- It is a performance measurement for the classification problems at various **decision threshold** settings of a model
- $ROC$ is used to get the best decision threshold depending on the needs
- $AUC$ is used to pick which classification model is the best
- $AUC$ is the probability that the model can distinguish TP and TN
	- $AUC = 1$ means the model is perfect
	![[auc=1.png]]
	- $AUC = 0.5$ means the model can't distinguish between TP and TN
	![[auc=0.5.png]]
	- $AUC = 0$ means the model is thinks TP as TN and vice-versa
	![[auc=0.png]]
- To use this in multi-class model, we must create the curve with one-vs-all style for each class
### R$^2$
- It's the percentage of variation explained by the relationship between two variables
- It's the square of correlation score
- $R^2 = \frac{var(mean) - var(fit)}{var(mean)} =\frac{\sum_{i=1}^{n} (y_i - \bar{y})^2 - \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}$ 
	- $y_i$ is the data point
	- $\hat{y}_i$ is the prediction by the model
	- $\bar{y}$ is the mean of the whole samples
- $R^2 = 0.8$ for example means that $80\%$ of the data variation can be explained by the relationship of the two variables
## Internal Measures (Clusters)
- All of the measurement below can be used to create a **graph** with the score in the $y$-axis and $K$ in $x$-axis
![[elbow method.png]]
- We pick the number of cluster that is the **elbow** of the curve
- In the example's case, it's 5
- This is called the **elbow method**
### Silhouette Method
- It's a method to measure how similar a point to its cluster compared to how different it is to its cluster's neighbor's points
- First, compute the similarity $a$ of the point $i$ to its comrades in the cluster $C_i$
	- $a(i) = \frac{1}{|C_i| - 1} \sum_{j \in C_i, j \neq i} d(i, j)$
- Then, compute the difference $b$ between $i$ and points in the closest neighboring cluster $C_k$
	- $b(i) = \min_{k \neq i} \frac{1}{|C_k|} \sum_{j \in C_k} d(i, j)$
- Finally, compute the score
	- $S(i) = \frac{b(i) - a(i)}{\max(a(i), b(i))}$
- The overall Silhouette score for the clustering is the average Silhouette score of all data points in the dataset
- It falls within the range $[-1, 1]$
	- A high Silhouette score (close to 1) indicates that the data points are well-clustered, and each data point is closer to members of its own cluster than to those of other clusters
	- A low Silhouette score (close to -1) suggests that data points are assigned to the wrong clusters
	- A Silhouette score near 0 means that clusters may overlap
- Usually, the score tier is 
	- Strong: 0.7 → 1
	- Medium: 0.5 → 0.7
	- Weak: 0.25 → 0.5
	- None: <0.25
### Within-Cluster Sum of Squares (WCSS)
- It measures the compactness or tightness of clusters
- For all points in each cluster, compute the square distance with the mean-centroid of each's cluster
	- $WCSS = \sum_{i=1}^{k} \sum_{j=1}^{n_i} (x_{ij} - \mu_i)^2$