- We have a collection of labeled samples $\{(x_i, y_i)\}_{i=1}^{N}$ where
	- N is the size of the collection
	- $x_i$ is the sample at index $i$ 
	- $y_i$ is the label of sample $x_i$ in **binary True (1) or False (0)**
- We still want to find a linear function of $x$ that maps to $y$, 
	- but the output of the model must be limited to only binary values
- To do this, we can use [[Activation Function#Sigmoid|Sigmoid Function]] that maps $x$ to range $[0, 1]$: $$f(x) = \frac{1}{1 + e^{-x}}$$
- We base our linear model to [[Activation Function#Sigmoid|Sigmoid Function]] to be: $$f_{w,b}(x) = \frac{1}{1 + e^{(-wx+b)}}$$
- To find the optimal model, we must have $w$ and $b$ such that the [[Maximum Log-Likelihood]] of the model is maximal: $$\arg\max_{w, b} \sum_{i=1}^{n} \left[ y_i \log(f_{w,b}(x_i)) + (1 - y_i) \log(1 - f_{w,b}(x_i)) \right]$$
- We can use [[Gradient Descent]] to find the optimal $w$ and $b$ 
