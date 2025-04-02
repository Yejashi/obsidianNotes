### Presentation 1
Which canonization algorithm works very well under the specific constraints of molecule canonization? Why?

Morgan canonicalization. It runs near linear time in best case and nlogn at worst case. It uses a hueristic spcalized for this particular problem. It also fails in more general canonicalization problems.

What strategy does NAUTY's algorithm employ to achieve canonization?

NAUTY's algorithms uses tree pruning to achieve canonicalization.

What are the five steps our program takes to generate an IUPAC name?
FInd the longest carbon chain.
Identify functional groups.


### Presentation 2

What is the parameter being optimized for out Level 1 approach?
THe scoring algirithm, BIC.

Why is it Max Min and not Min Max?
Selects a parent/child candidate with the maximum of the mimumum associations across conditioning sets.

Who is the father of Eugenics?

Sir Francis Galton


### Presentation 3
What are the 3 fundamental layers in GNNs?
- Message passing layer
- Local pooling layer
- Global pooling layer

What are the limitations of GNNs?
- Limited expressiveness
- Long range dependencies
- Over smoothing

What is the problem with too many message passing layers?
- Over smoothing occurs. 

email: kneupan1@vols.utk.edu

### Presentation 4

What is the difference between IP (integer program), MILP (mixed integer linear programm), and LR (linear relaxation)?
- IP, all the decision variables are required to be integers.
- MILP some of the decision variables are required to be integers.
- LP, take away all the integers requirements and making continious.

What type of graph can we convert an MILP and MINLP to?

What graph property can we leverage to improve performance on unit constraint problems (specifically with loss of ac line contingencies)?