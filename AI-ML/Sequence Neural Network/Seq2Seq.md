![[seq2seq.png]]
- We want to translate a sequence input to another sequence output
- For example:
	- Machine Translation
	- etc
- The most famous seq2seq architecture for this is called **Encoder-Decoder** architecture
	- By **separating** **Encoder** and **Decoder**, we separate 
		- The task of learning the input (**Encoder**)
		- The task of learning how to map the input to the output (**Decoder**)
## Encoder
![[encoder_statq.png]]
- The **Encoder** consists of $l$ layers of [[RNN]] like [[LSTM]] or [[GRU]]
- The number of timesteps $t$ and inputs are the same as the length of the input sequence
- Each *token* of the sequence is represented as a **vector embedding** (e.g. word embedding)
- The point of Encoder is to get a **Context Vector** as the vector representation of the input
- The resulting [[LSTM#^b01cd8|Short-term Memory]] and [[LSTM#^2ffe0d|Long-term Memory]] is considered as the **Context Vector** of the encoder
## Decoder
![[decoder statq.png]]
- The **Decoder** consists of $l$ layers of RNN like LSTM or GRU
- It takes the Short-term Memory and Long-term Memory of the Context Vector as its own Short-term Memory and Long-term Memory
- Its goal is to decode the Context Vector with the help of the **label senquence** as its **inputs**
- The $l$ last hidden states of the Decoder are fed into a [[Fully Connected Layers]]
- The resulting vector of the Fully Connected Layers is fed into a [[Activation Function#Softmax|Softmax Layer]] to get the **output token** at timestep $t$
- The input for the next timestep $t+1$ is
	- **Training**: The label token at $t$
	- **Inference**: The output token of $t$
- The Decoder will stop when it reaches the prediction token of `<EOS>` or it hits a maximum output length
## The Paper
- The original paper used
	- $160,000$ input tokens for the encoder
	- $80,000$ input tokens for the encoder
	- $1,000$ embedding values per token
	- $4$ layers with $1000$ LSTMs per layer
	- $80,000$ softmax outputs