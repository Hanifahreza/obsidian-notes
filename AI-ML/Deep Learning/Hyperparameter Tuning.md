- Techniques to find the optimal hyperparameter of a model given a data
- For example, we would like to optimize the hyperparameters `max_depth` and `n_estimators` of RandomForestClassifier
![[hyperparam tuning ilus.png]]
## Grid Search
![[gridsearch.gif]]
- Exhaustive brute-force search
- Given a defined hyperparameter space:
````python
n_estimators = [10, 50, 100, 200]
max_depth = [3, 10, 20, 40]
````
- It would yield the following models:
  ````python
RandomForestClassifier(n_estimators=10, max_depth=3)
RandomForestClassifier(n_estimators=10, max_depth=10)
RandomForestClassifier(n_estimators=10, max_depth=20)
RandomForestClassifier(n_estimators=10, max_depth=40)

RandomForestClassifier(n_estimators=50, max_depth=3)
RandomForestClassifier(n_estimators=50, max_depth=10)
RandomForestClassifier(n_estimators=50, max_depth=20)
RandomForestClassifier(n_estimators=50, max_depth=40)

RandomForestClassifier(n_estimators=100, max_depth=3)
RandomForestClassifier(n_estimators=100, max_depth=10)
RandomForestClassifier(n_estimators=100, max_depth=20)
RandomForestClassifier(n_estimators=100, max_depth=40)

RandomForestClassifier(n_estimators=200, max_depth=3)
RandomForestClassifier(n_estimators=200, max_depth=10)
RandomForestClassifier(n_estimators=200, max_depth=20)
RandomForestClassifier(n_estimators=200, max_depth=40)
````
- Obviously it's inefficient
## Random Search
![[randomsearch.gif]]
- Instead of providing discrete values for the search space,
	- We provide a **statistical distribution** for each hyperparameter
- The algorithm will randomly select a value from the distribution
````python
from scipy.stats import expon as sp_expon
from scipy.stats import randint as sp_randint

n_estimators = sp_expon(scale=100)
max_depth = sp_randint(1, 40)
````
- We define how many iterations will the algorithm search for the best hyperparameter
	- In each iteration, it will **randomly** select a combination of hyperparameter values and test it
## Bayesian Optimization
![[bayesian optimization.gif]]
- **Bayesian Optimization** aims to find the hyperparameters that optimize an **objective function**
	- Typically the validation performance of a machine learning model.
- It uses a probabilistic model (commonly a Gaussian Process) to model the unknown objective function
	- This model provides an estimate of the function's behavior and its uncertainty
- An **acquisition function**, such as Expected Improvement (EI) or Probability of Improvement (PI), quantifies how beneficial it is to evaluate the objective function at different hyperparameter configurations
- The acquisition function balances between 
	- Exploration (sampling unexplored areas) and
	- Exploitation (sampling where the objective function is likely to be optimal)
- It's a sequential optimization
	- It starts with an initial set of hyperparameters and their corresponding objective function values
	  - At each step, the acquisition function suggests a new hyperparameter configuration to evaluate.
	  - The objective function is then evaluated at this configuration, and the result is used to update the probabilistic model
	  - The process repeats until a stopping criterion is met (e.g., a budget of evaluations is exhausted).
### Pros
- Bayesian Optimization is efficient and effective. It often requires fewer evaluations of the objective function compared to grid search or random search.
- It adapts to the function's behavior and focuses on promising hyperparameter configurations.
