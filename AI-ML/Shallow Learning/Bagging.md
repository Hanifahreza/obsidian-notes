- It can handle [[Data Imputation|missing values]]
## Bootstrapping
- Make $n$ new datasets by randomly selecting rows from the original dataset (duplicate allowed)
- For each new datasets, create tree based on $k$  features of all available features
- Bootstrapping and feature selection are used to reduce variance
- Selecting $k$ that is close to the square root or log of the number of features is the best
## Aggregating
- Predict using all individual classifiers (trees)
	- For classification:
		- Class with the most votes by all the trees win
	- For regression:
		- Average the result of all trees
## Bagging
![[random forest.png]]
- **Bagging** = **Bootstrapping** + **Aggregating**