![[lr decays.png]]
- Change learning rate based on time during training
- $t$ = epoch
- $s$ = step
- $\lambda$ = decay rate
## Performance Decay
  - Drop the learning rate when the validation error stops dropping
## Piece-Wise Constant
- $$\eta_t = \eta_i \space \text{if} \space t_i \leq t \leq t_i+1$$
	-  $t_i$ = A set of time points where $\eta$ is adjusted
## Step Decay
  - In step decay, the learning rate is reduced by a fixed factor after a predefined number of epochs or steps
  $$\eta = \eta_0 \cdot \lambda^{t / s}$$
## Exponential Decay
  - Exponential decay reduces the learning rate exponentially over time
  $$\eta = \eta_0 \cdot e^{-\lambda \cdot t}$$
## Polynomial Decay
- $$\eta_t = \eta_0(\beta_t+1)-\alpha$$
	- Usually
		- $\alpha = 0.5$
		- $\beta = 1$
- Polynomial decay with usual α and β is equivalent to **square root schedule**: $$\eta_t = \frac{\eta_0}{\sqrt{t + 1}}$$
## Time-Based Decay
  - The learning rate is reduced based on a time-dependent schedule
   $$\eta = \frac{\eta_0}{1 + \lambda \cdot t}$$
## Cosine Annealing
  - Cosine annealing uses a cosine function to cyclically vary the learning rate.
  $$\eta = \frac{\eta_0}{2} \left(1 + \cos\left(\frac{\pi \cdot t}{\max(t)}\right)\right)$$
## Warm-Up
- Quickly increase $\eta$ and then gradually drop it
![[warmup lr.png]]
## Cyclical Decay
- Increases and decreases $\eta$ multiple times to escape local minima
- The half-cycle can be chosen according to how many restarts are suitable for our training budget
![[cyclical decay.png]]