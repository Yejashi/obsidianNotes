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

Then F(n) = (n-1) + (1/n) * $\sum$ (i = 1, n) [F(i-1)]