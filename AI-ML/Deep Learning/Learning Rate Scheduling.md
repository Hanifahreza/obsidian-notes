- Change learning rate based on time during training
## Performance Scheduling
  - Drop the learning rate when the validation error stops dropping
## Step Scheduling
  - In step scheduling, the learning rate is reduced by a fixed factor after a predefined number of epochs or steps
  $$\eta = \eta_0 \cdot \text{factor}^{\text{epoch} / \text{step}}$$
## Exponential Scheduling
  - Exponential scheduling reduces the learning rate exponentially over time
  $$\eta = \eta_0 \cdot e^{-\text{decay} \cdot \text{epoch}}$$
## Time-Based Scheduling
  - The learning rate is reduced based on a time-dependent schedule
   $$\eta = \frac{\eta_0}{1 + \text{decay} \cdot \text{epoch}}$$
## Cosine Annealing
  - Cosine annealing uses a cosine function to cyclically vary the learning rate.
  $$\eta = \frac{\eta_0}{2} \left(1 + \cos\left(\frac{\pi \cdot \text{epoch}}{\text{max\_epochs}}\right)\right)$$