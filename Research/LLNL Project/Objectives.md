In a single sentence the objective of this endeavor is to track and report the behavior of optimization passes during compilation.

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

###### Why an analysis pass?
We are observing and not transforming.

This means the optimization are applied by clang's optimization pipeline through llvm. We simply want to monitor the transformations that are considered. An analysis pass can observe the results of other passes and collect statistics about their behavior.

###### Where does the pass need to go?
We need to inject a custom analysis pass into the pass manager pipeline. This pass would observe the IR before and after each transformation pass and log any changes or failures.
