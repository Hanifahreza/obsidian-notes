## Preliminary Notes
![[candy soda venn.png]]
- $P(C'|S)$ means 
	- Instead of computing probability of C in the set universe,
		- $P(C) = \frac{6}{14} = 0.43$
	- We limit our scope to compute the probability in S's circle area
		- $P(C|S) = \frac{2}{7} = 0.28$
	- Which also means
		- $P(C|S) = \frac{P(C)}{P(S)}$
## Bayes Theorem
![[bayes visual.png]]
- Consider 
	- $H$ is **hypothesis** and $E$ is **evidence**
	- The left vertical column as $H$
	- The rest of the square that's not part of $H$ as $\sim H$
	- The blue areas as $E$
	- The blue part of $H$ as $P(E|H)$ which means
		- It's part of $H$ that satisfies $E$
- Then:
	- Probability of $E$ that satisfies $H$ is equal to
		- Probability of H **AND** probability of $H$ that satisfies $E$
		- Divided by probability of $E$ no matter it's part of $H$ or not
		- This can be visualized as the **light blue area** / **whole blue area**
	- Mathematically:
		- $P(H|E) = \frac{P(H)\cdot P(E|H)}{P(E)}$
			- $P(H|E)$ is called the **Posterior**
			- $P(E|H)$ is called the **Likelihood**
			- $P(H)$ and $P(E)$ is called the **Prior** 