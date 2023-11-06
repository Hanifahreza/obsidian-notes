## Solutions
### Missing Value / Outliers
- Discard rows with missing values or outliers out
- Infer the missing value from neighboring data ([[Data Amputation]])
- Fill/change with a zero/constant
- Fill with mode for categorical data
### Data Noise 
- Smoothing
### Data Transformations
- Summarize data
- Generalize data
- Make new attribute from the given ones
![[data normalization.png]]
- Normalization (Min-Max Scaling)
	- Change the range of the data to $[0, 1]$
	$$x' = \frac{x - \min(X)}{\max(X) - \min(X)}$$
	- Sensitive to outliers
- Standardization (Standard Scaling) ^ba3b7c
	- Use z-score such that the transformed data has
		- mean = 0  
		- std = 1
	- $$x' = \frac{x - \mu}{\sigma}$$
		- $\sigma$ is std
		- $\mu$ is mean 
- Data Selection
	- Pick relevant rows or columns from the dataset
	- Pick columns with high correlation with target variable 
	- Pick rows relative to total size (50%, 75%, etc)
	- Pick rows so that the number of rows is nice (1000, 500, 69, etc)