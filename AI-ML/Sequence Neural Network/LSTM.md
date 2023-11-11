## Idea
- To tackle [[Vanishing & Exploding Gradient Problem]] in vanilla [[RNN]], separate the hidden states of the previous cells into 2 inputs:
	- **Hidden State** (Short-term memory) $H_{t-1}$ ^b01cd8
		- This is the output of a cell in timestep $t$
		- It only runs from a cell to the next cell
	- **Memory Internal State** (Long-term memory) $C_{t-1}$ ^2ffe0d
		- This memory runs from the beginning of the network until the end without any learnable parameters
- This also helps the network to remember hidden states from long time ago (long term-memory)
## Gates
![[lstm.png]]
### Forget Gate
- It determines *how much* of the long-term memory should be "forgotten" with the output of a [[Activation Function#Sigmoid|Sigmoid function]]
- The mathematical representation is: $$F_t = \sigma(W_{xf}X_t + W_{hf}H_{t-1} + b_f)$$
### Input Gate & Node
- **Input Gate** determines *how much* of the current short-term memory should be added to the long-term memory
- **Input Node** determines *what* should be added to the long-term memory
- The mathematical representation is: $$\begin{align*}& I_t = \sigma(W_{xi}X_t + W_{hi}H_{t-1}+b_i) \\& \tilde{C}_t = \tanh(W_{xc}X_t + W_{hc}H_{t-1}+b_c) \end{align*}$$
- The long-term memory is updated by forget gate output $F_t$ and current input node output $\tilde{C}_t$ with: $$C_t = F_t \odot C_{t-1} + I_t \odot \tilde{C}_t$$
### Output Gate & Hidden State
- **Output Gate** determines *how much* of the potential next short-term memory should be added
- **Hidden State** is the $\tanh$ of the updated long-term memory that will be the potential next short-term memory
- The mathematical representation is: $$\begin{align*}& O_t = \sigma(W_{xo}X_t + W_{ho}H_{t-1}+b_o) \\& H_t = O_t \odot \tanh(C_t) \end{align*}$$
## Bidirectional LSTM
![[bi-lstm.png]]
- To also consider future inputs for the current input, we can add another LSTM network that run reversely
- The output of each $t$ is the sum or concatenation of $H_t$ of the two LSTMs
## Pros
- Eliminates [[Vanishing & Exploding Gradient Problem]]
- Can remember input from long time ago
- With Bi-LSTM, it can consider the input from the future
## Cons
- High computational cost
- Requires large amount of data
- Difficult to interpret