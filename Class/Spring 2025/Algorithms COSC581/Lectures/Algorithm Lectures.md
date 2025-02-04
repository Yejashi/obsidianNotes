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
Algorithm 1
- Identify the smallest, then the next smallest, etc
- COntinue until we find the nearest $n/2$ smallest.

Algorithm 2
- Sort the file
- Use the item at location $n/2$ .

Algorithm 3:
- Pseudo-randomly pick a small set of elements
- Use their median as a proxy

Algorithm 4.
- Break the file into subfiles
- Find the median of each suffle
- Compute the median of medians

The median of medians approach
- CHoose an r > 1 (for file size)
- As we'll see, it turn out that 5 is a good choice
- Divide L into n/r subfiles
- Find the median of each subfile
- Find the median of medians

Obserbe:
- Every element o A is at most M