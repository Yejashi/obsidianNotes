General Objective: For each function, extract how many transformation passes:
- Were attempted
- Succeeded
- Failed

##### What is needed to achieve this?
We need an analysis pass that monitors optimization attempts since most optimizations, at least the ones we care about, are applied at the middle-end phase of the LLVM pipeline.

What needs to be tracked:
- Transformations attempted
	- This includes all optimization attempts (i.e loop unrolling, inlining, dead code elimination, etc)
- Transformations Failed
	- This should happen when a transformation is skipped or doesn't apply (i.e a loop is not unrolled for `x` reason.)
- Transformation Succeeded
	- This happens when a particular transformation successfully modifies the IR.


##### Why a transformation pass over an analysis pass?

