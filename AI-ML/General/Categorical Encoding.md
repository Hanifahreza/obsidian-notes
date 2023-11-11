- Encode **discrete variables** into **numerical variable**
## One-Hot Encoding 
![[one-hot.png]]
- Create **new features** out of **every unique values**
- Assign $1$ and $0$ to each new feature depending on the old feature
- **Works fine** when the number of **unique values** is **small**
- **Works terrible** when the number of **unique values** is **huge**
## Label Encoding
![[label encoding.png]]
- Assign each unique value with a number 
- It **works terrible** if the data is not actually ordinal
	- This is because an algorithm will think there's a semantic meaning in having higher value despite the values in the feature is not numerically comparable
## Target Encoding
![[target encoding.png]]
- The number assigned to each unique value depends on the value of the **target feature**
- For example, we assign the **mean** of the **target feature** of every unique value as its numerical value 
- This is kinda good, but it can underestimate unique values that has very small appearance
- It also causes **data leakage** because the encoding depends on the target feature
## Bayesian Mean Encoding
- It's a **Target Encoding** method, but it uses **Weighted Mean** for each unique value
- The mathematical formula is: 
- $$W = \frac{n \cdot \mu_v + m \cdot \mu_o}{n + m} $$
	- $W$ is the weighted mean that will be the assigned value
	-  $\mu_v$ is the mean of the target variable in rows with the current value
	- $n$ is the number of rows with the current value
	- $\mu_o$ is the mean of the target variable
	- $m$ is a hyperparameter which decides the importance of $\mu_o$
- This is good, but it causes **data leakage** because the encoding depends on the target feature
## K-Fold Target Encoding
- Divide the data into $K$ folds
- Do **Bayesian Mean Encoding** for each row, but only considers the **target feature** values in **other folds**
- This stops **data leakage** since it doesn't depend on the **target feature's value in the same row**
## Catboost (Ordered Target) Encoding
- Slide each row from top to bottom one by one
- Assign the encoding value for the row with the formula: 
- $$W = \frac{\lambda + 0.05}{n + 1}$$
	- $W$ is the assigned value
	- $\lambda$ is the number of previous visited rows that has the same value with the current value *AND* has value $1$ for the target feature
- If the target feature is **numerical**, stratify it into bins and assign $1$ and $0$ to create a **categorical** version of the feature