![[RNN.png]]
- **Recurrent Neural Networks** (RNNs) are a class of artificial neural networks that allow **previous outputs** to be used as inputs while having **hidden states**
![[description-block-rnn-ltr (1).png]]
- The output at a timestep can be a representation of
	- **Hidden State** $y_t$: The output at $t$ 
	- **Activation** $a_t$: One of the inputs for $t+1$ 
- For each **timestep** $t$ $$\begin{align*}& a_t = \sigma_1(W_{aa} \cdot a_{t-1} + W_{ax} \cdot x_t + b_a) \\& y_t = \sigma_2(W_{ya} \cdot a_t + b_y) \end{align*}$$
- All of the **parameters** are **shared** across the **timesteps**
## Types of RNN
- $T_x$ is the number of inputs
- $T_y$ is the number of outputs
### One-to-One
![[tnn.png]]
- $T_x = T_y = 1$
- Basically a traditional neural network
### One-to-Many
![[otm-rnn.png]]
- $T_x = 1, \space T_y > 1$
- One input for the prompt 
- Produce a sequence of outputs
- Example application:
	- Music generation ($x$ = a muscial note, $y_t$ = next notes)
### Many-to-One
![[mto-rnn.png]]
- $T_x > 1, \space T_y = 1$
- Input is a sequence
- Output is just one value
- Example application:
	- Classification
### Many-To-Many
![[mtm-rnn.png]]
- $T_x > 1, \space T_y > 1$
- Input is a sequence
- Output is also a sequence
- Example application:
	- [[Named Entity Recognition]]
	- [[Machine Translation]]
## Cons
- Slow computation
- Information from long time ago is lost
- Cannot consider future input for current state
- Prone to [[Vanishing & Exploding Gradient Problem]]