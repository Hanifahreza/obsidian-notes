## Idea
- **BERT** is a stack of [[Transformer#Encoder-Decoder|Transfomer's Encoders]] 
- The output of the Encoders is used to as **word embedding**
- The resulting **word embedding** can be used for tasks such as:
	- Machine Translation
	- Question Answering
	- Sentiment Analysis
	- Text Summarization
	- Etc
- The steps to train BERT to produce the desired word embedding are:
	- **Pretraining** BERT such that it understands the language input
	- **Fine-Tune** BERT to a specific task
## Pretraining
![[bert pretraining.png]]
- BERT pretraining consists of 2 separate tasks:
	- **Masked Language Modelling (MLM)**
		- It's given sentences with some words being masked with `[MASK]` token
		- The goal is to predict the right word for each mask
	- **Next Sentence Prediction (NSP)**
		- It's given 2 sentences $A$ and $B$
		- Decides with binary classification if the 2 sentences follow or not
- These 2 tasks are trained **simultaneously** 
  ![[bert 2.png]]
  - When embedding the input, beside considering the [[Transformer#Embedding Layer|Token Embedding]] and the [[Transformer#Positional Embedding|Positional Embedding]], we also consider **Segment Embedding**:
	    ![[segment embedding.png]]
	  - This embedding captures the **order** of each input **sentence**