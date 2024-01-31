- Likelihood, denoted as $L(\theta | x)$, is a function of the model parameters $(\theta$) given the observed data $(x)$.
- It is often expressed as the [[Probability Density Function|PDF]] or [[Probability Mass Function|PMF]] of the data, 
	- With the model parameters treated as variables
- Likelihood measures
	- How well the model with specific parameter values, explains the observed data
	- It quantifies the compatibility between the model and the data
- Likelihood can be used to compare different models or hypotheses
	- The model that maximizes the likelihood given the data is often preferred as the best-fitting model
## ML Context
- Likelihood of a model is the probability of all predictions in $f(y_i | x_i)$ that a model produce is true irl
- Basically it measures how good a model fit the data
- The formula is:
$$\mathcal{L}(y | x) = \prod_{i=1}^{n} f(y_i | x_i) = \prod_{i=1}^{n} ​p_i ^{y_i}​​ ⋅ (1−p_i​)^{1−y_i}​$$
- Think of it as the multiplication of all probabilities that the model produce (AND operation)