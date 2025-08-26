## Aug 1 2025

When finding the the other strand of DNA
- Find its complements (A<--->T)
- Then reverse it
	- This is because 5 prime have to be on the left and 3 prime on right

For neiandrethal do p(A) * p(T) ...

2 sequences
- calculate probability of a t c g's.

Markov stuff
- C A T A T
- Count al necluitodes
	- There are CA AT TA AT
- P(T | A) = 1
- P(C | A) = 0
- P(G | A) = 0

Downoad NC_0014161


## Aug 26 2025

Two kinds of homology:
- ORthologous - speciation based split
	- changes in same repo
- Paralagous - gene duplication-basedsplit
	- fork or clone

Global alignment
- also called pairwise alignmenet
- Intuitive goal:
	- related sequences will share many (most?) character. To maximizr this we introduce gaps represented by "-"
S: CAT
T: AT-
T' - AT

Moving the gap increased the alignment

Two simple rules:
1. when you have a gap, it must correspond with a non gap character. cant have gap with a gap.
2. To distinguish good alignment from bad, we introduce scoring function.
Alignment lenth cant be longer than sum of two sequences.

