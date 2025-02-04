### Lecture 5

How do measure ?
- Worst cast
- Average case
- Stability
- Other? For example, out of core.

Average case analysis of quicksort
- Assume keys are distinct
- Assume all permutations are equally likely

Let F(n) denote the average number of comparisons required

Then F(n) = (n-1) + (1/n) * $\sum$ (i = 1, n) [F(i-1) + F(n-i])]
 
 which by symmetry = (n-1) + (2/n)$\sum$ (i=1,n)[F(i-1)]
 - this is a first order homogenous recurrence
 - It requires a change of variable
 - Then uses asymptotics (~) to convert a series to an itegral.
 - And finally find that F(n) is about 1.39 nlog2n   

Back to quicksort
- Its average case is excellent.
	- But the analysis assumes that keys are distinct, and that all permutation are equally likely.
	- MOreover, the worst case is truly awful.
		- Can we address this?
		- And if so, is the cure worse than the disease.
Algorithm
- Identify the smallest, then the next smallest, etc
- COntinue until we find the nearest $n/2$ smallest.

Time complexity:
