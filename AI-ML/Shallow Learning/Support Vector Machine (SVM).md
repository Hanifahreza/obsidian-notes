- We want to separate samples into 2 classes
- We can do this by drawing a 1D line or 2D, 3D, etc hyperplane **threshold** to separate both classes
- The shortest distance between the samples and the threshold is called **margin**
![[svm margin.png]]
- The closest sample of each class to the margin is called the **support vector**
- However, if the samples are not linearly separable, we can use the [[Kernel Trick]]
## Hard Margin Classification
![[hard_margin1.png]]
- Our goal here is to **maximize the margin**
- Given the threshold hyperplane is $\vec{w} * x-b = 0$ 
	- The positive support vector is $\vec{w} * x - b = 1$
	- The negative support vector is $\vec{w} * x - b = -1$
- We want to know how much should we walk from a point in the threshold to reach a support vector in $\vec{w}$ direction (perpendicular)
- So if we want to reach the positive support vector, 
	- $\vec{w} * (\vec{x} + k\frac{\vec{w}}{||w||}) - b = 1$ where $k$ is scalar unit
	- $\vec{w} * \vec{x} + \vec{w} * k\frac{\vec{w}}{||w||} - b = 1$ and since $\vec{w} * x = b$,
	- $k\frac{\vec{w} * \vec{w}}{||w||} = 1$ which means $k = \frac{1}{||w||}$
	- This means, the margin size is $\frac{2}{||w||}$
	- So to maximize margin size, we need to **minimize $||w||$**
- There's also an extra constraint
	- If $y_i = 1$ => $\vec{w} * \vec{x} - b \geq 1$
	- If $y_i = -1$ => $\vec{w} * \vec{x} - b \leq -1$
	- To acommodate these constraints, $y_i (\vec{w} * \vec{x_i} -b) \geq 1$
- So the final goal is to **minimize $||w||$** and **$b$** such that for all $i$,
	- $y_i = (\vec{w} * \vec{x_i} -b) \geq 1$
## Soft Margin Classification
- Hard margin sucks because it can't handle noises and outliers due to its greedy nature
- To mitigate this, we introduce **hinge loss**
	- $L = max(0, 1-y_i(\vec{w} * \vec{x} - b))$ 
		- $y_i$ is the true class 
		- $\vec{w} * \vec{x} - b$ is the score
	- When the score is correct, $L$ will be $0$
	- When the score is different than the truth, $L$ will be positive
	- When $0 < y_i(\vec{w} * \vec{x} - b) < 1$, it means the sample is in the margin range which means a light penalty 
- Beside that, we also want to maximize the margin by minimizing $||w||$
- So now, the goal is to pick $\vec{w}$ and $b$ such that we **minimize** the 
  (**average hinge loss**) $+ \lambda||w||^2$ 
	- $\lambda$ is a hyperparameter that
		- If it's small, the margin might be bigger in price of more error
		- If it's big, the margin might be smaller but there would be less error
- To update $w$, we can use the formula
	- $w' = w + \alpha (y_i * x_i - 2\lambda w)$ 
	- $\alpha$ is the learning rate