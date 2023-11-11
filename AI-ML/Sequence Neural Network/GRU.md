## Idea
- [[LSTM]] is great but what if in our task long-term memory isn't that important and we want the model to be lighter?
- **GRU** offers a comparable performance with LSTM with faster computation
	- This is because GRU only uses 2 gates instead of 3 in LSTM
## Gates
![[gru.png]]
### Reset Gate 
- It determines *how much* of previous state should be "remembered" with the output of a [[Activation Function#Sigmoid|Sigmoid function]]
- The mathematical representation is: $$R_t = \sigma(W_{xr}X_t + W_{hr}H_{t-1} + b_r)$$
### Update Gate
- It determines *how much* of the new state is just gonna be a copy of the old state
- The mathematical representation is: $$Z_t = \sigma(W_{xz}X_t + W_{hz}H_{t-1} + b_z)$$
### Candidate Hidden State
- The candidate for the hidden state of the cell at $t$ is the $R_t$-filtered $H_{t-1}$ combined with the input $X_t$ $$\tilde{H}_t = \tanh(W_{xh}X_t + W_{hh}(R_t \odot H_{t-1}) + b_h) $$
### Hidden State
- Integrate update gate $Z_t$ to the candidate hidden state $\tilde{H}_t$ to get $H_t$ $$H_t = Z_t \odot H_{t-1} + (1-Z_t) \odot \tilde{H}_t$$
## Bidirectional GRU
![[bi-gru.png]]
- To also consider future inputs for the current input, we can add another GRU network that run reversely
- The output of each $t$ is the sum or concatenation of $H_t$ of the two GRUs
## Pros
- Eliminates [[Vanishing & Exploding Gradient Problem]]
- Lighter than [[LSTM]]
- Better for smaller datasets compared to [[LSTM]]
- Competitive performance against [[LSTM]] if capturing long time ago state isn't that important
- With Bi-GRU, it can consider the input from the future
## Cons
- Can't incorporate states too much long time ago