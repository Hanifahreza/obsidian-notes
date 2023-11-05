- Add a regularization parameter $\lambda$ to reduce the importance of weights $w$ in the model
- This will reduce variance which prevent overfitting
- It also helps to find the optimal model when the number of training data is less than the number of features
- Use [[K-Fold Validation]] to get the best $\lambda$ hyperparameter by testing different values for it
## Ridge Regression (L2 Regularization)
### Linear Regression
- Change the loss function from
	- $\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$
- To this
	- $\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 + \lambda w^2$
### Logistic Regression
- Change the loss function from
	- $\sum_{i=1}^{n} \left[ y_i \log(f_{w,b}(x)) + (1 - y_i) \log(1 - f_{w,b}(x)) \right]$
- To this
	- $\sum_{i=1}^{n} \left[ y_i \log(f_{w,b}(x)) + (1 - y_i) \log(1 - f_{w,b}(x)) \right] + \lambda w^2$
## Lasso Regression (L1 Regularization)
- Similar to Ridge, except we add $\lambda |w|$ instead of $\lambda w^2$
- The big difference is that with increasing $\lambda$, 
	- Lasso can eventually hit a total slope of 0
	- Ridge can only go asymptotically to 0
	- Hence, Lasso is better for killing useless features