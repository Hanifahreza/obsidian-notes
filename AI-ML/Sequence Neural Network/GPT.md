- **GPT** only use [[Transformer#Encoder-Decoder|Decoder of Transformer]] and stack them to **generate response** from a **prompt**
![[gpt-dec.png]]
- Each input token is used to generate the **next token**
- When the decoder predicts **`<EOS>`** as the **next token**, it starts the **response generation**
- Each prediction token will be used as the input to predict the next prediction token
- This is done until it predicts the **`<EOS>`** token for the **response**