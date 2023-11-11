## Vanilla Autoregression
- An **Autoregressive** ($\text{AR}$) model of order $p$
	- Is a **time series model** that expresses the current value as a linear combination of its past values
- The general form of an $\text{AR}(p)$ model is given by:
- $$X_t = \sum_{i=1}^{p} \phi_i X_{t-i} + \epsilon_t$$
	- $X_t$ is the current value of the time series at time $t$
	- $\phi_i$ is the $i$-th Autoregressive coefficient
	- $X_{t-i}$ is one of the past values of the time series
	- $\epsilon_t$ is the white noise error term at time $t$
## Latent Autoregression
- **Latent Autoregressive Model** (LARM) is a probabilistic model that combines autoregressive structures with latent variables
- It keeps some hidden summary $h_t$ of past observations
	- At the same time, it also update $h_t$ in addition to estimate of $X_t$ ($\hat{X}_t$)
![[latent autoregression.png]]
- It can be expressed as: $$\begin{align*} &
\hat{X}_t = P(X_t|h_t) \\& h_t = g(h_{t-1}, X_{t-1}) \end{align*}$$