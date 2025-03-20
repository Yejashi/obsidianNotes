### Presentation 1
Which canonization algorithm works very well under the specific constraints of molecule canonization? Why?

Morgan canonicalization. It runs near linear time in best case and nlogn at worst case. It uses a hueristic spcalized for this particular problem. It also fails in more general canonicalization problems.

What strategy does NAUTY's algorithm employ to achieve canonization?

NAUTY's algorithms uses tree pruning to achieve canonicalization.

What are the five steps our program takes to generate an IUPAC name?
FInd the longest carbon chain.
Identify functional groups.
