- Simplify a data with many features to less features
## Techniques
### Principal Component Analysis (PCA)
- Compute the average point of all data points
- Make the average point as the origin the graph and suit the points with the new origin
- Draw a line that goes through the origin
- Project all points to the line
- Rotate the line until the **sum of squared distance of the projected points to the origin** (**SSD**) is **maximum**
- The line is called **PC{number}** (e.g. PC1)
- For the next PCs, just create new lines perpendicular to the previous line
- Rotate the line so it's straight
- The average SSD of PC1 ($\frac{SSD}{n-1}$) is called the **Eigenvalue** of PC1
- If we have $n$ features, there are $n$ PCs
- The variation contribution of each PCs is the PC's Eigenvalue divided by the sum of all PC's Eigenvalues
- Pick the most important PCs to create a new lower dimension data
### T-SNE
- Todo
## Pros
- **Curse of dimensionality**  states
	- As the number of feature increases, a classifier’s performance increases until an optimal number of features is reached
	- Adding more features past the optimal number of features will instead degrade the performance
- To eliminate redundant unhelpful features
- To visualize data with more than 3 dimensions in 1-3 dimensional space
## Cons
- There might be some information loss
- Harder to interpret
