## Why EDA?
• We need to familiarize with a new dataset: 
	• How many **attributes**, and of what kind?
	• Are there any **missing values**?
	• How are the values **distributed**?
	• Is our dataset **imbalanced**? 

• Hunting for something interesting:
	• Are there any **outliers**?
	• Are there any **correlations** between attributes?
	• How do the **distributions** compare between **different samples**?
## Descriptive Statistics
### Central Tendency
- Mean, Median, Mode
### Measures of Variation
- Range (Max - Min)
- Inter-Quartile Range (IQR):
	- Q1 (lower quartile): 25th percentile
	- Q2 (median): 50th percentile 
	- Q3 (upper quartile): 75th percentile
	- IQR = Q3 - Q1
- Variance & STD
	- Variance: 
		- Average of the squared deviation of the observations from the mean
		- For population, the formula is
			- $\sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2$
		- For sample, the formula is
			-  $\sigma^2 = \frac{1}{N-1} \sum_{i=1}^{N} (x_i - \mu)^2$
	- STD: ^516c1d
		- Square root of variance
		- Easier to interpret than variance since it's on the same scale with the original data
	- If variance/std is high, then the dataset has large variability
- Outliers
	- An observation that lies an abnormal distance from other values in a random sample from a population
	- Outliers are samples that are:
		- $x_i < Q_1-1.5*IQR$ or 
		- $x_i > Q_3 + 1.5*IQR$
### Skewness
- Measure of asymmetry of the data around the mean
![[skew.png]]
- When a distribution is skewed,
	- The mode remains the most commonly occurring value
	- The median remains the middle value in the distribution
	- But the **mean** is generally **"pulled"** in the **direction of the tails**
- $\text{Skewness} = \frac{1}{N} \sum_{i=1}^{N} \left(\frac{x_i - \mu}{\sigma}\right)^3$
### Kurtosis
- Measure of how many samples are at the left and right tails of a bell-curve 
- The higher the kurtosis, the flatter the curve
![[kurtosis.png]]
- Types of kurtosis:
	- Leptokurtic: Kurtosis > 3
	- Mesokurtic: Kurtosis = 3, normal distribution
	- Platykurtic: Kurtosis < 3
	![[kurtosis2.png]]
- High kurtosis indicates the presence of outliers
- $\text{Kurtosis} = \frac{1}{N} \sum_{i=1}^{N} \left(\frac{x_i - \mu}{\sigma}\right)^4$
### Correlation
- Technique to investigate the relationship between two variables
- Measures the strength of the association between the two variables
- Correlation coefficient returns a value between -1 and 1
	- -1 denotes strongest negative correlation
	- 0 denotes no correlation
	- 1 denotes strongest positive correlation
![[correlation.png]]
- Pearson: $r = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2} \sqrt{\sum_{i=1}^{n} (y_i - \bar{y})^2}}$