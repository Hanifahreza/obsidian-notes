## Idea
![[attention connection.png]]
- The problem with vanilla [[Seq2Seq]] is that it only encodes the input into a single Context Vector
	- If the input is a very long sequence, it's possible for the long-term memory to forget earlier tokens
- **Attention** solves this problem by adding a **connection** in each timestep $t$ of the **encoder** to the **decoder**
## Attention
### Similarity Pooling
![[attention similarity.png]]
- We want to compute similarity score between *current timestep*'s input of the **decoder** with *all* timesteps' input of the **encoder** from *every layer*
- The most commonly used similarity score is [[Similarity & Distance Measurements#Cosine Similarity|Cosine Similarity]] but **without the denominator** to save computational cost
	- Basically just the **dot product**
### Computing Attention
![[attention 2.png]]
- The result of the dot products will be $n$ values with $n$ being the length of the input sequence
- We feed all of the results to a [[Activation Function#Softmax|Softmax Layer]] to compute the **percentage** of **each encoded input token** we **should use when decoding**
- The outputs of the softmax is then used to scale the encoded input tokens at each timestep to its respective softmax output 
- Then, we sum all of the weighted encoded input tokens to get the **Attention** of the decoder's input token at timestep $t$
### Decoding
![[attention 3.png]]
- The Attention at $t$, together with the hidden state of the decoder at $t$, is then fed to a [[Fully Connected Layers]] with Softmax to determine the output token
- By integrating Attention to the final FC layers, all of the input encoder tokens have a say in how the final decoder output is computed