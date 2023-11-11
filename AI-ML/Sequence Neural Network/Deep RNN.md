## Idea
- Stack multiple [[LSTM]]s or [[GRU]]s on top of each other
## Structure
![[deep rnn.png]]
- For each timestep $t$,
	- There are $l$ layers of hidden states
- The mathematical representation is 
- $$H_t^{(l)} = \phi(W_{xh}^{l} H_t^{(l-1)} + W_{hh}^{(l)} H_{t-1}^{(l)} + b_h^{(l)} $$
	- $\phi$ is the activation function
- The output of the network at timestep $t$ is based on the hidden state of the last hidden layer $l$ at timestep $t$ $$ O_t = W_{hq}H_t^{(l)} + b_q $$