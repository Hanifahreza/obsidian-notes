## Definition
- Cluster samples in data such that the 
	- Intra-cluster distance is minimized
	- Inter-cluster distance is maximized
- This task is **unsupervised**
- Use one of the [[Similarity & Distance Measurements#Distance|distance measurement]] to determine distance
## Algorithms
### Hierarchical Agglomerative
#### Algorithm
- With $N$ data points, there are $N$ clusters initially containing only a single data point
- We want to make a **dendogram** which is a **cluster-merging history tree**
![[dendogram.png]]
- Count similarity distance between each cluster to find 2 closest clusters
- Join the found 2 closest clusters
- Repeat again until all data points are in the same cluster
- Make a horizontal cut in the dendogram to extract the needed number of clusters
#### Proximity Measures
- But how to choose which point in a multi-points cluster as the representation of that cluster in measuring distance?
- Here are the methods:
	- **Single Link** (MIN prox) / (best linkage)
		- Pick two closest elements between the two clusters
		- Usually creates a long chain in clustering
	- **Complete Link** (MAX prox) / (worst linkage)
		- Pick two furthest elements between the two clusters
		- Usually creates a "sphere" in clustering (crowding)
	- **Average Link**
		- Average all pairwise distances of the two clusters ($O(N^2)$)
		- Less affected by outliers
	- **Centroid Distance**
		- Distance between the centroid of the two clusters
#### Pros
- Produce a dendogram that can give insights on relationship between clusters
- No need to define how many clusters we want
- Easy to interpret
- Good for small to medium-sized datasets
#### Cons
- Expensive computation cost ($O(N^3)$)
- Need to use memory to store dendogram
- Sensitive to noise and outliers
### K-Means Clustering
#### Algorithm
- Take $K$ initial points from available data points
- These are now the cluster means/centroids
- For each non-centroid point, compute the distance with each cluster mean 
- Every point is then assigned to the nearest cluster mean
- Get a new centroid for each cluster by taking the mean point of the cluster
- Repeat until **threshold** is reached ($K$ with the lowest total variance) 
- **Threshold** criterion (Convergence)
	- No/Minimum reassignments
	- No/Minimum change of centroid
#### Pros
- Easy to understand and implement
- Efficient complexity: $O(\text{iterations} * K * \text{samples} * \text{dimensions})$
	- Since $K$, $\text{dimensions}$, and $\text{iterations}$ are usually small, it's considered linear
- Only applicable when **mean** can be defined
- Categorical version of K-Means is [[K-Modes]]
#### Cons
- Need to specify number of clusters $K$
- Sensitive to outliers
	- This is because it assumes a hypersphere cluster due to the use of an arithmetic mean and the distance to the mean as the definition of the cluster
- Data has different densities between clusters
- Sparse / other non-spherical shapes are not applicable
	- Generally shapes that don’t approximate a form where all points on the surface are equidistant to the center of the shape will not work
- Not applicable for non-linearly separable clusters
![[non-linear-separable.png]]
- To deal with this, we can use [[Kernel Trick]] to bring it to higher dimension
![[kernel trick.png]]
### DBSCAN
#### Algorithm
- Scan all data points
	- If a data point is neighboring $K$ points in radius $\epsilon$, label it as a **core point**
- Scan all core points
	- Assign the core point as part of a cluster
	- Assign all neighboring points in radius $\epsilon$ as part of the cluster
- Points that are not assigned to a cluster is labeled outlier
![[dbscan.png]]
#### Pros 
- No need to define how many clusters we want
- Robust to outliers
- Can identify arbitrary shapes unlike K-Means
- Can handle clusters with varying density
#### Cons
- Sensitive to hyperparameter $K$ and $\epsilon$
- Not really effective for highly sparse data
- Expensive computation ($O(N^2)$)