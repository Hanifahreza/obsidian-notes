- We want to maximize [[Likelihood]], since the greater the likelihood, the likelier the probabilities the model produce is right irl
- To search for the optimal parameter $x$ such that $\mathcal{L}$ is maximum, we first convert the multiplication loop to addition loop with logarithm:
$$\mathcal{L}(y | x) = \sum_{i=1}^{n} \log{f(y_i | x_i)}$$
- By converting it to log, it will be easier to compute since addition is easier than multiplication