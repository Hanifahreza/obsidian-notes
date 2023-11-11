- It's a method mostly used for **OCR** and **Voice Recognition**
  ![[ctc pipeline.png]]
- We want to map
	- The input vector which is the output of an [[RNN]]
	- Characters in the label text
![[ctc problem.png]]
- However a character in the label text can be mapped to many input vector's values
- This results in a lot of duplicate characters
- **CTC** solves this by introducing **blank character "-"**
## Encoding Text
- When the output has a lot of duplicate we want to erase all of the duplicate characters
- But what if the duplicate is actually right such as the word "hello"
- We use the blank character "-" to indicate true duplicates
- The encoding possibility examples are:
	- **"to"** -> "---ttttooooo", "-t-o-", "to"
	- **"too"** -> "---ttttto-ooo", "-t-o-o-", "to-o", **but not** "too"
## CTC Loss
![[ctc loss.png]]
- We create a matrix for every possible input w.r.t every timesteps
- To calculate the probability score for a path, just multiply the scores:
	- "aa" = $0.4 \cdot 0.4 = 0.16$
	- "a-" = $0.4 \cdot 0.6 = 0.24$
	- "--" = $0.6 \cdot 0.6 = 0.36$
- The loss is simply the $-\log$ of the probability score of the path
## Decoding
- There are a lot of algorithms to get the best path
  ![[best-path-decod.png]]
- The most common is a **greedy** algorithm called **best path decoding** with 2 key steps:
	- It calculates the best path by taking the most likely character per time-step
	- It undoes the encoding by
		- Removing the duplicate characters
		- Removing all blanks in the path