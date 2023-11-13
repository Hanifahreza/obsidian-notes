## Similarity
### Set Similarity
#### Jaccard 
$$J(A, B) = \frac{|A \cap B|}{|A \cup B|}$$
### Cosine Similarity
$$ C(A, B) = \frac{A \cdot B}{\|A\| \cdot \|B\|} = \frac{\sum_{i=1}^nA_iB_i}{\sqrt{\sum^n_{i=1}A^2_i} \cdot \sqrt{\sum_{i=1}^n}B^2_i}$$
- The numerator is what actually computes the similarity
- The denominator is used to normalize the output range to $[-1, 1]$
- Often used for text or word embedding
## Distance
### Minkowski
$$D_p(A, B) = (\sum_{i=1}^{n} |A_i - B_i|^p)^{\frac{1}{p}}$$
![[chebyshev.png]]
#### Manhattan
- When $p = 1$
$$D_1(A, B) = \sum_{i=1}^{n} |A_i - B_i|$$
- Less sensitive to outliers  
#### Euclidean
- When $p = 2$
$$D_2(A, B) = \sqrt{\sum_{i=1}^{n}(A_i - B_i)^2}$$
#### Chebyshev
- When $p = \infty$
$$D_{\infty}(A,B) = max_i |A_i - B_i|$$