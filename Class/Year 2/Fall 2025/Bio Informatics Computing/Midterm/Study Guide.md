
#### **Reverse compliment**
- DNA comes in 5'->3' format.
- To get reverse complement:
	- Get matching nucleotide for every nucleotide (A->T C->G)
		- It is currently in 3'->5' format
	- Reverse to turn into 5'->3' format.
##### Study Guide Question 2
![[Pasted image 20250929130223.png]]
Solution:
- 5' CATAT 3'
- 3' GTATA 5'
- 5' ATATG 3'

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
##### Study Guide Question 2
![[Pasted image 20250929144733.png]]
Solution:
- D 
	- The maximum value of the last row and column

