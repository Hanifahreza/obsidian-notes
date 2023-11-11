## How to Handle Missing Values?
### General
- **Drop** the **rows** with missing values
- **Drop** the **feature** with too many missing values
- Create a model (**estimator**) with the feature as the $y$ and other features as $x$
	- Usually [[K-Nearest Neighbors (KNN)]]
### Numerical
- Replace with **mean**, **median**, or **mode** of the feature
### Categorical
- Replace with the mode of the feature