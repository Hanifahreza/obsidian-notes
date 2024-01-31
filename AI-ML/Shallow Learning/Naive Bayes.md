- It uses [[Bayes Theorem]] as the basis for its prediction
- Called **"Naive"** because it assumes that the features used in classification are independent of each other
## Multinomial Naive Bayes
- It's Naive Bayes done to a data with [[Multinomial Distribution]]
- Usually used for text data with features corresponding to word counts
- The prediction of an input is [[Maximum Log-Likelihood|the most likely class given the data]] $$\hat{y} = \arg\max_{y} P(y) \prod_{i} P(x_i | y)$$
	- $\hat{y}$ is predicted class
	- $y$ is the ground truth class
	- $x_i$ is individual feature (i.e. word in a sentence)
	- $P(x_i | y)$ is calculated by dividing the occurrence of word $x_i$ in class $y$ by occurrence of all words in class $y$
- If we encounter a word we haven't met before, it would turn the whole likelihood to 0
	- **Laplace smoothing**: To prevent this, add 1 to all word count 
## Gaussian Naive Bayes
- It's Naive Bayes done to a data with [[Normal Distribution]]
- Prediction is made by finding the class with the highest posterior probability using Bayes' theorem: $$\hat{y} = \arg\max_{y} P(y) \prod_{i} P(x_i | y)$$
	- $(P(x_i | y)$ is the probability of feature $x_i$ given class $y$ and is modeled as a Gaussian distribution.
## Pros
- Computationally efficient  
- can handle high-dimensional data with many features
- It's especially useful when you have limited data
- It can be a good baseline algorithm for classification tasks
## Cons
- Naive 
- It's not well-suited for capturing complex relationships between features
