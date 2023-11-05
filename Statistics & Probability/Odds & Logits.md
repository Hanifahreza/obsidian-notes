## Odds
 - **Odds** is the ratio of something happening and something not happening
 - Mathematically it's:
	 - $\text{odds} = \frac{P}{1-P}$
## Logit
- **Logit** is basically just log of odds
- Mathematically it's:
	- $\text{logit} = \log(\frac{P}{1-P})$
- The reason this is useful is because:
	- The range of the odds of something not happening is $[0, 1]$
	- Meanwhile, the range of odds something is happening is $[1, \infty]$
	- This is a very huge asymmetric disparity
	- Logit transforms it such that the range of both of them is symmetrical