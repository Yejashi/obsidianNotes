General Objective: For each function, extract how many transformation passes:
- Were attempted
- Succeeded
- Failed

##### What is needed to achieve this?
We need a transformation pass that monitors optimization attempts since most optimizations, at least the ones we care about, are applied at the middle-end phase of the LLVM pipeline.

What needs to be tracked:
- Transformations attempted
	- This includes all optimization attempts (i.e loop unrolling, inlining, dead code elimination, etc)

