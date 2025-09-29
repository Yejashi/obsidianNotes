#### **Reverse compliment**
- DNA comes in 5'->3' format.
- To get reverse complement:
	- Get matching nucleotide for every nucleotide (A->T C->G)
		- It is currently in 3'->5' format
	- Reverse to turn into 5'->3' format.
##### Study Guide Multiple Choice Question 1
![[Pasted image 20250929130223.png]]
Solution:
- 5' CATAT 3'
- 3' GTATA 5'
- 5' ATATG 3'

![[Pasted image 20250929152901.png]]
Solution:
- 5' ATGACATTTG 3'
- 3' TACTGTAAAC 5'
- 5' CAAATGTCAT 3'

#### **Alignment**
![[Pasted image 20250929131247.png]]
##### Global Alignment
![[Pasted image 20250929131401.png]]
![[Pasted image 20250929135944.png]]
- Definition: Aligns sequences end-to-end, from the first nucleotide/amino acid to the last
- Needleman–Wunsch algorithm
- When used:
	- When sequences are of similar length and you want to compare them across their entire span

##### End-gap Free Alignment
![[Pasted image 20250929141424.png]]
![[Pasted image 20250929142059.png]]
- Also semi-global
- Definition: A special case of semiglobal. The alignment is optimized without penalizing leading or trailing gaps
- When used:
	- When we dont want to penalize leading or trailing gaps
	- subtrings
##### **Local Alignment**
![[Pasted image 20250929142904.png]]
- Definition: Finds the best matching sub-sequences within the larger sequences
- Smith–Waterman algorithm
- When used:
	- When sequences differ in length or only have shared conserved regions

**Note:**
- S1: Set the top row and left column to 0:
	- This allows alignments to start anywhere
- S2: Calculate the alignment between gaps, diag and choose the max between (match, mismatch, gap, zero)
- S3: When doing a trace back start from the largest numbers anywhere in the matrix
![[Pasted image 20250929144501.png]]
##### Study Guide Multiple Choice Question 2
![[Pasted image 20250929144733.png]]
Solution:
- D 
	- The maximum value of the last row and column
##### Study Guide Multiple Choice Question 4
![[Pasted image 20250929145526.png]]
Solution:
- b
![[Pasted image 20250929150249.png]]

##### Study Guide Short Response E
![[Pasted image 20250929152344.png]]
**Global alignment** tries to align **entire sequences from end to end**, even if that means introducing gaps or mismatches. It’s best when the two sequences are of **similar length and overall related**.
- tldr: emphasize _entire sequences_
**Local alignment** looks for the **best matching subsequences** inside the two sequences. It doesn’t force the whole sequences to line up — it just finds the **highest-scoring region of similarity**, which is useful if only part of the sequences are related.
- emphasize _best matching subsequences_
#### **Multinomial models** 
A multinomial model is any probabilistic/statistical model that assumes data (counts, frequencies, categories) are generated from a multinomial distribution.

Basically every point has a probability and the chance you get something depends on that array of probabilities.

##### Study Guide Question 3
![[Pasted image 20250929145250.png]]
Solution:
- P(A) = 2/4 P(T) = 1/4 P(G) = 1/4
- Answer = a =  P(A) = 2/4
##### Study Guide Short Response A
![[Pasted image 20250929150612.png]]
Dinucleotices are pairs of consecutive nucleotidecs (e.g. AG, CT, etc). The dinucleotide frequence tells you the probability of a given Dinucleotide occurring within a sequence. It is calculated by taking the total number of occurances of a given sequence and dividing by the number of dinucleotides in the sequence.

##### Study Guide Short Response C
![[Pasted image 20250929151222.png]]
- To calculate this we must first find the number of nucleotides where A occurs in the first position. (x)
- Then given these nucleotides we must count how many of them are TA. (y)
- Then we can calculate y/x to get the probability.
- In this case:
	- X = [AT, AT] = 2
	- Y = [AT, AT] = 2
	- Y / X = 1

#### Markov Models
A Markov model is a way to describe systems that evolve step by step, where the future depends only on the present, not on the full past history.

![[Pasted image 20250929154514.png]]

Structure:
- A Markov model has a finite set of states.
- The system starts in some state (often chosen according to a probability distribution
- At each step, it moves to the next state based on transition probabilities that depend only on the current state (not how you got there).
- This makes it a memoryless process (the “Markov property”).


#### Hidden Markov Models (HMM)
In a standard Markov chain, you can **see the states directly** (e.g., “today is sunny, tomorrow will be rainy”).

But in many real problems, the **states are hidden** — you can’t observe them directly. Instead, you only see **outputs (emissions)** that depend on the hidden states.

HMM Structure:
- Hidden  States
	- Finite set of states you don’t directly observe (e.g., coding vs non-coding DNA, fair die vs loaded die)
	- They evolve according to a Markov chain with **state transition probabilities**
- Observations (emissions)
	- At each step, the hidden state generates an **observable symbol** (e.g., a nucleotide, a die roll, a word in text)
- Initial distribution
	- Probabilities of starting in each hidden state
Key property:
- You cannot see the states; you only see the outputs
- The model links the outputs back to the hidden process that produced them

![[Pasted image 20250929160010.png]]

In the dishonest casino the hidden states is whether the die is loaded or fair. The emission is the roll from the current die with the probability distribution as shown above.

![[Pasted image 20250929160246.png]]