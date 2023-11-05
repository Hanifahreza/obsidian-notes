## Similarity
### Set Similarity
#### Jaccard 
- $J(A, B) = \frac{|A \cap B|}{|A \cup B|}$
### Cosine Similarity
- $C(A, B) = \frac{A \cdot B}{\|A\| \cdot \|B\|}$
- Often used for text
## Distance
### Minkowski
- $M(A, B) = (\sum_{i=1}^{n} |A_i - B_i|^p)^{\frac{1}{p}}$
![[chebyshev.png]]
#### Manhattan
- When $p = 1$
	- $M(A, B) = \sum_{i=1}^{n} |A_i - B_i|$
- Less sensitive to outliers  
#### Euclidean
- When $p = 2$
	- $E(A, B) = \sqrt{\sum_{i=1}^{n}(A_i - B_i)^2}$
#### Chebyshev
- When $p = \infty$
	- $D_{\infty}(A,B) = max_i |A_i - B_i|$