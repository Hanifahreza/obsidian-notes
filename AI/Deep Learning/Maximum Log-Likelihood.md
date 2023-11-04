- Likelihood of a model is the probability of all predictions in $f(y_i | x_i)$ that a model produce is true irl
- The formula is:
  > 				 $\mathcal{L}(y | x) = \prod_{i=1}^{n} f(y_i | x_i)$
- Think of it as the multiplication of all probabilities that the model produce (AND operation)
- We want to maximize this since the greater the likelihood, the likelier the probabilities the model produce is right irl
- To search for the optimal parameter $x$ such that $\mathcal{L}$ is maximum, we first convert the multiplication loop to addition loop with logarithm:
	> 							$\mathcal{L}(y | x) = \sum_{i=1}^{n} \log{f(y_i | x_i)}$