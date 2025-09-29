
#### **Reverse compliment**
- DNA comes in 5'->3' format.
- To get reverse complement:
	- Get matching nucleotide for every nucleotide (A->T C->G)
		- It is currently in 3'->5' format
	- Reverse to turn into 5'->3' format.
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
- Also semi-global
- Definition: A special case of semiglobal. The alignment is optimized without penalizing leading or trailing gaps
- 
##### **Local Alignment**
- Definition: Finds the best matching sub-sequences within the larger sequences
- Smith–Waterman algorithm
- When used:
	- When sequences differ in length or only have shared conserved regions
