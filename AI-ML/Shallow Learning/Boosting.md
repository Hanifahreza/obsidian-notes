- Unlike [[Bagging]], creating a classifier depends on the previous classifier
- The goal is to create another classifier that covers the mistakes of previous classifier
- It also can handle [[Data Imputation|missing values]]
## AdaBoost
### Training
- Create a weight ($w$) for each sample as $\frac{1}{n}$ 
![[adaboost weight.png]]
- Create a tree using the technique in [[Decision Tree]] which consists of only a root node and two children (nothing more)
	![[stump.png]]
- Total Error ($TE$) of the tree is the sum of the sample weight of all wrongly classified samples
- Create a new variable called $\delta$ (amount of say the tree will have for the final decision)$$\delta = \frac{1}{2}\log(\frac{1-TE}{TE})$$
- Update the sample weights
	- For all samples that are not correctly classified: $$w_i' = w_ie^\delta$$
	- For all samples that are correctly classified: $$w_i' = w_ie^{-\delta}$$
- Normalize so all $w'$ add up to $1$
- Create the next tree with **weighted gini** as the basis using [[Decision Tree]] technique $$\text{Weighted Gini} = 1 - \sum_{i=1}^{n} w_i P(x_i)^2$$
- Repeat making trees with the new $w$ until the `max_tree` is reached
### Predict
- Compare the sum of all $\delta$ of trees in each class
- For example: 
	- Sum of all $\delta$ of trees that say `yes` is $3.69$
	- Sum of all $\delta$ of trees that say `no` is $2.45$
	- Since $\delta_{yes} > \delta_{no}$, the result is `yes` 
## Gradient Boost
### Regression
#### Training
- Create a single leaf with the average of target feature ($\hat{y}$) as the initial prediction value $y$ for all samples
- Create a new feature called `residual` ($r$) as $y-\hat{y}$
- Create a tree using the technique in [[Decision Tree]] to predict `residual` ($\hat{r}$) with `max_deph` usually in $[8, 32]$ 
- For all leafs:
	- Compute the `residual prediction` ($\hat{r}$) of the leaf as the mean of the `residuals` in the leaf
- Update the prediction for each sample as
- $$y' = y + \alpha \hat{r}$$
	- $\alpha$ is the learning rate
- Repeat making tree with the new $y'$ until the `max_tree` is reached OR there's no improvement in the residuals
#### Predict
- The output is at first the initial average of target feature
- Insert the input to all of the trees to predict the `residuals`
- The prediction is the sum of the initial average with all of the predicted `residuals` from all trees
### Classification
#### Training
- Create a single leaf with the [[Odds & Logits#Logit|Logit Function]] $log(\text{odds}) = log(n_{yes}/n_{no})$ as the initial prediction value $y$ for all samples
	- If it's multi-class, do this for every class
- Convert the prediction with [[Activation Function#Sigmoid|Sigmoid Function]] to probability
	- If it's multi-class, use [[Activation Function#Softmax|Softmax Function]] with inputs from all classes' trees
- Create a new feature called `residual` ($r$) as $y-\hat{y}$ with `yes = 1` and `no = 0`
- Create a tree using the technique in [[Decision Tree]] to predict `residual` ($\hat{r}$) with `max_deph` usually in $[8, 32]$ 
- For each leafs of the newly created tree
	- for each value in the leaf ($i$), convert it to a probability with $$\frac{\sum r}{\sum (\text{prev prob})_i (1-(\text{prev prob})_i)}$$
		- $(\text{prev prob})_i$ is the previous probability of the residual's sample 
- Update the prediction for each sample as
- $$y' = y + \alpha \hat{r}$$
	- $\alpha$ is the learning rate
	- Then, convert it to 
- Convert the prediction with [[Odds & Logits#Logit|Logit Function]] to probability
	- If it's multi-class, use [[Activation Function#Softmax|Softmax Function]] with inputs from all classes' trees
- Repeat making tree with the $y'$ until the `max_tree` is reached OR there's no improvement in the residuals
#### Predict
- The output is at first the initial prediction
- Insert the input to all of the trees to predict the residuals
- The prediction is the sum of the initial prediction with all of the predicted probability from all trees
## XGBoost
### Regression
#### Training
- Assign $0.5$ as the initial prediction value $y$ for all samples
- Collect all `residual` ($r = y-\hat{y}$ ) to a single leaf
- Calculate `similarity_score` ($s$) of the leafs as
- $$s = \frac{(\sum r)^2}{n + \lambda}$$
	- $\lambda$ is regularization hyperparameter
- Loop from the first 2 samples with lowest $x$ to the next 2 lowest, and so on:
	- Take the average of the 2 samples
	- Use the average as the condition to split the `residual` values to left and right child 
	- Compute $s$ of the left and right child
	- Compute gain $$g = s_{left} + s_{right} - s_{root}$$
- Sort the data based on $x$
- Take the average of 2 samples with the highest $g$ as the branch condition of the tree
- Repeat for the left and right child until the `max_depth`of the tree is reached
- Take a number for hyperparameter $\gamma$
- For every branch in the tree:
	- Calculate $\gamma - g$ 
	- If it's negative, prune the branch and repeat the check for the root of the branch
	- Else, let it and its root go
- For all leafs:
	- Compute the output value as $$\hat{y} = \frac{\sum r}{n + \lambda}$$
- For all samples:
	- Update the prediction as $$y' = y + \epsilon \hat{y}$$
- Repeat making tree with the new $y'$ with
#### Predict
- The output is at first the initial prediction $0.5$
- Insert the input to all of the trees to predict the residuals
- The prediction is the sum of the initial average with all of the predicted residuals from all trees
### Classification
- Assign $0.5$ as the initial prediction value $y$ for all samples
- Collect all `residual` ($r = y-\hat{y}$ ) to a single leaf with `yes = 1` and `no = 0`
- Calculate `similarity_score` ($s$) of the leafs as
- $$s = \frac{(\sum r)^2}{\sum [(\text{prev prob})_i (1-(\text{prev prob})_i)] + \lambda}$$
	- $\lambda$ is regularization hyperparameter
	- $(\text{prev prob})_i$ is the previous probability of the residual's sample 
	- $\sum [(\text{prev prob})_i (1-(\text{prev prob})_i)]$ is also called `cover`
	- XGBoost has hyperparameter `minimum_cover`
		- So a node with `cover` < `minimum_cover` is not allowed
- Sort the data based on $x$
- Loop from the last 2 samples with lowest $x$ to the previous 2 lowest, and so on:
	- Take the average of the 2 samples
	- Use the average as the condition to split the `residual` values to left and right child 
	- Compute $s$ of the left and right child
	- Compute gain $$g = s_{left} + s_{right} - s_{root}$$
- Take the average of 2 samples with the highest $g$ as the branch condition of the tree
- Repeat for the left and right child until the `max_depth`of the tree is reached
- Take a number for hyperparameter $\gamma$
- For every branch in the tree:
	- Calculate $\gamma - g$ 
	- If it's negative, prune the branch and repeat the check for the root of the branch
	- Else, let it and its root go
- For all leafs:
	- Compute the output odd prediction value as $$\hat{y}_{odd} = \frac{\sum r}{\sum [(\text{prev prob})_i (1-(\text{prev prob})_i)] + \lambda}$$
- For all samples:
	- Update the prediction with
		- Transform the previous probability prediction to odd with [[Odds & Logits#Logit|Logit Function]] $$y_{odd} = log(\frac{y}{1-y})$$
		- Update the odd $$y_{odd}' = y_{odd} + \epsilon \hat{y}_{odd}$$
		- Convert $y_{odd}'$ to probability prediction $y'$ with [[Activation Function#Sigmoid|Sigmoid Function]]
- Repeat making tree with the new $y'$ with
#### Predict
- The output is at first the initial probability prediction of $log(\frac{0.5}{1-0.5}) = 0$
- Insert the input to all of the trees to predict the residuals
- The prediction is the sum of the initial prediction with all of the predicted probability from all trees
### Optimizations
#### Approximate Greedy Algorithm
- Instead of looping every 2 samples to compute a branch threshold candidates,
	- Divide the data to **quantiles** and **use the quantile** to compute branch threshold candidates
	- The quantiles are also just an approximate to save computation cost
	- The quantiles are also weighted 
- This is only used when the data is huge
#### Parallel Learning
- Computation for each quantiles can be done in parallel
- This is only used when the data is huge
#### Sparsity-Aware Split Finding
- Handle rows with missing features but known target feature
- Basically just ignore the missing features and create 2 separate $g$ when computing gain
	- $g_{left}$ is the gain when the missing features row's residuals are put into the left child
	- $g_{right}$ is the gain when the missing features row's residuals are put into the right child
	 - Pick the best $g$ and move on as usual
## CatBoost
- Initialize the predictions for all rows as $0$
- Calculate the residuals of all rows
- Use [[Categorical Encoding#Catboost (Ordered Target) Encoding|Ordered Target Encoding]] to encode the categorical features
- Sort the non-target features ascending
  ![[catboost sort.png]]
- Create thresholds from middle value of bins in the sorted features
  ![[catboost stub.png]]
- For each thresholds
	- Create a binary trees with initial values for its left and right children as $0$ from the thresholds
	- Make a new column for the leaf outputs
	- For each row
		- When we arrive at a row, update the leaf output with the average of the values
		- Insert the residual to the tree and update the output of the child as the average of the values
	-  Calculate [[Similarity & Distance Measurements#Cosine Similarity|Cosine Similarity]] of the residuals and the leaf outputs
- Select the threshold with that produce the highest similarity
- For each row, update the prediction with $$y' = y + \alpha \cdot \text{leaf} $$
- Update the residual
- Return the discrete values to all categorical features
- Do all of the steps except the 1st 