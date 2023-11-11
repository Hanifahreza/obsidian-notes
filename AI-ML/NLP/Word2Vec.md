- We want to **transform** a **word** into a **vector** to represent the word
- The vector must also capture the semantic meaning of the word
- So words that are closely related should have close vectors
- **Word2Vec** utilizes 2 models to do this:
	- **Skip-Gram** model
	- **Continous Bag of Words (CBOW)**
## Skip-Gram
- It assumes that a word can be used to generate its surrounding words
- For example take the sequence 
``` python
["the", "man", "loves" , "his", "son"]
```
- If we take "loves" as the center of the sequence with `window_size`= 2, it will model the sequence as $$\begin{align*}& P(\text{"the"}, \text{"man"}, \text{"his"}, \text{"son"} \space | \space \text{"loves"}) \\& 
  = P(\text{"the"} \space | \space \text{"loves"}) \cdot P(\text{"man"} \space | \space \text{"loves"}) \cdot P(\text{"his"} \space | \space \text{"loves"}) \cdot P(\text{"son"} \space | \space \text{"loves"}) \end{align*}$$
  TODO
  