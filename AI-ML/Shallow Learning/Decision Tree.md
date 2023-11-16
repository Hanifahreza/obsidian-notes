![[decision tree.png]]
- We want to create a binary tree that can assign a data point to a class based on conditions
- We need an algorithm to learn what are the suitable condition for each node that **maximize information gain**
- This means we need to **minimize [[Entropy]]** or [[Entropy#Gini Index|Gini Index]] for each node
## Classifier
- Loop all features $x_i$ to get what feature to use as the condition for the current node
- Loop all unique values $x_{ij}$ in the feature to determine which value to use as the condition
- Compute the [[Entropy]] or [[Entropy#Gini Index|Gini Index]] of left and right child if we make a decision boundary based on the value ($x_i \leq x_{ij}$ for example)
	- Then compute the **information gain** of the value $$\text{IG} = E(\text{parent})-\sum{w_i E(\text{child}_i)}$$
		- $E$ is the entropy
		- $w_i$ is the weight of the child based on the number of samples in the child compared to total sample
- Continue the above steps with recursion to the left and right child until reaching `max_depth` or the samples in the node is $\leq$ `min_samples_split`
- When we reach the leaf node, decides what class it belongs by taking the mode of the samples' class
## Regressor
- The algorithm is the same as the classifier
- The differences are:
	- Minimize **average sum squared error** AKA **variance** $$\frac{\sum_{i=1}^{n}(y_i - \hat y)}{n}$$
	- The leaf node value decision is the average of all samples' values
## Pros
- Easy to interpret
- Can handle mixed discrete and continous input
- Perform automatic feature selection
- Relatively robust to outliers
- Fast to fit and scale well for large datasets
## Cons
- Don't predict really accurately (due to its greedy nature)
- Unstable: 
	- Small changes in input data can cause huge effects