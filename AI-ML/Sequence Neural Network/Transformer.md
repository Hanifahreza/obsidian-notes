## Idea
- [[Seq2Seq]] model with [[LSTM]] and [[Attention]]'s long-term memory is still not enough for very long sequence
- It's also heavy and not really efficient
- **Transformer** solves these problems with **Self-Attention**
## Embedding Layer
![[trans-word-embed.png]]
- Make a normal neural network with $n_{we}$ *identity* [[Activation Function]]s $$F(x) = x$$
- Feed each token of the input sequence to the layer
- Each output of the activation function serves as a value of the **embedding vector**
- Usually there are **hundreds** or **thousands** of values in an embedding vector
## Positional Embedding
![[pos embed.png]]
- **Positional Embedding** is used to retain the information of the position of a token in the input sequence
- We create $n_{we}$ different **sine** and **cosine** functions to match with the size of the embedding vector
- If a **token's position** in the sequence is $i$, 
	- then each **value $j$** of the positional embedding is $f_j(i)$
		- $f_j$ is the $j$-th sine-or-cosine function
- We **sum element-wise** the **word embedding** and the **positional embedding** to get the vector representation of the tokens
## Self-Attention
![[self attention.png]]
- The goal of self-attention is to **calculate the similarity** of each **token** to **all other tokens** *including itself* 
- By doing this, it can know the relationship and references of each word to other words
- It does this by creating **Query**, **Key**, and **Value** for each token from the **embedding**
### Query
![[trans-query.png]]
- **Query** vector of length $n_{we}$ is created by scaling the embedding values with weight parameters
- The parameters used are **shared** across tokens
- This vector will be used when we want to compute the **similarity** of **its token** w.r.t **other tokens** using **dot product**
### Key
![[trans-key.png]]
- **Key** vector of length $n_{we}$ is created by scaling the embedding values with weight parameters
- The parameters used are **shared** across tokens
- This vector will be used when we want to compute the **similarity** of **another token** w.r.t **its token** using **dot-product**
- The similarity result vector of current token with other tokens is fed into a [[Activation Function#Softmax|Softmax Function]]
	- The results are the influence percentage of each tokens on how to encode current token
### Value
![[trans-value.png]]
- **Value** vector of length $n_{we}$ is created by scaling the embedding values with weight parameters
- The parameters used are **shared** across tokens
- This vector will be used as the **real representation** of the current token in **computing the attention** of the current token
- The Values of *each token* are scaled using the corresponding **outputs of the Key's Softmax**
- The **scaled values** are then **summed** to get the **Attention vector** of the current token
- This is done to *every input token* to gain their Attention vectors
### Parallel Computing
- With good GPU, the computation of **Queries**, **Keys**, and **Values** can be done in parallel
- This saves training and inference time efficiently
### Multi-Head Attention
![[multi-head attention.png]]
- We can stack the **QVK Attention cells** to create a **Multi-head Attention**
- The original paper stacked **8** self-attention cells
## Residual Connection
![[trans-residual.png]]
- The original **embedding vector** is brought to the end of the **QVK Attention cell** to be summed with the output of the cell
- This is done using [[ResNet#Skip Connections|Residual Connection]] to bypass the cell
- By doing this, it can go deeper without triggering [[Vanishing & Exploding Gradient Problem]]
## Encoder-Decoder
- The process below is done for all **Decoder**'s input tokens from `<EOS>` to `<CLS>`
### Encoder-Decoder Query & Key
![[trans-enc-dec-key-query.png]]
- Create new **QVK Attention cell** for each **input token** of the **Decoder**
	- During training, the QVK cell use **Masked Self-Attention** instead of the usual Self-Attention
	- This algorithm only considers similarity of current token with **preceding tokens** and **itself** when computing Attention
- For each **QVK Attention cell** in **Encoder**, create **Key** vector
- For each **QVK Attention cell** in **Decoder**, create **Query** vector
- Compute similarity vector of each **Query** vector in **Decoder** with all all **Keys** in the **Encoder** using **dot product** 
- Feed the result to Softmax
### Encoder-Decoder Value
![[enc-dec value.png]]
- For each **QVK Attention cell** in **Encoder**, create **Value** vector
- Scale it with the previous Softmax outputs to get the **Encoder-Decoder Attention**
### Encoder-Decoder Residual
![[enc-dec residual.png]]
- Create a **Residual Connection** for the original **Decoder**'s input **embedding** to the top of the **Encoder-Decoder QVK cell** and sum with its result
### Encoder-Decoder FC Layer
![[enc-dec-fc.png]]
- The output vector of the **Encoder-Decoder Residual** is fed into a [[Fully Connected Layers]] with Softmax to determine the output token