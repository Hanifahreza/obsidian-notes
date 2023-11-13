- The idea of **entropy** is to quantify how *hard* is an information to be compressed
- Basically an information with stream of only "a" is much easier to be *predicted*, hence easier to be *compressed* with less factor of *surprise* than an information which contains bunch of characters
- For a distribution $P$ its entropy, $H[P]$ , is defined as: $$H[P] = -\sum_{i=1}^{n} P(x_i) \log(P(x_i))$$
## Cross Entropy
- **Cross entropy** from distribution $P$ to $Q$ is how much *surprise* we would get if we expect distribution $Q$, but instead what we get is distribution $P$ 
- Mathematically it's defined as: $$H[P, Q] = -\sum_{i=1}^{n} P(x_i) \log(Q(x_i))$$
- In the context of ML, we can think of it as the *difference* between the real distribution and the distribution produced by a model
- This means we want the cross entropy to be as little as possible
## Gini Index
- Entropy can be hard to compute due to the existence of $\log$
- We can instead use Gini Index which is easier to compute: $$1 - \sum_{i=1}^{n} P(x_i)^2$$