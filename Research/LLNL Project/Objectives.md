In a single sentence the objective of this endeavor is to track and report the behavior of optimization passes during compilation.

Initial Objectives: For each function, extract how many transformation passes:
- Were attempted
- Succeeded
- Failed

What needs to be tracked:
- Transformations attempted
	- This includes all optimization attempts (i.e loop unrolling, inlining, dead code elimination, etc)
- Transformations Failed
	- This should happen when a transformation is skipped or doesn't apply (i.e a loop is not unrolled for `x` reason.)
- Transformation Succeeded
	- This happens when a particular transformation successfully modifies the IR.

### What is needed to achieve this?
This project doesn't directly fit into the usual categories of transformation or analysis passes. 

However, it seems that LLVM's modular structure and its pass management system allow for such meta-level tracking.

To even attempt this, i need to:
- Familiarize myself with the new Pass Manager (NPM), as LLVM deprecated the legacy Pass Manager.
- Learn how passes interact, including their dependencies and how analysis results are preserved.

Where to Integrate?
- **At the Pass Manager Level**: This involves hooking into the Pass Manager to observe all passes applied globally or per function.
- **Within a Custom Pass**: This involves running after the -O3 pipeline and retroactively collecting metadata about transformations.




















We need an analysis pass that monitors optimization attempts since most optimizations, at least the ones we care about, are applied at the middle-end phase of the LLVM pipeline.


###### Why an analysis pass?
We are observing and not transforming.

This means the optimization are applied by clang's optimization pipeline through llvm. We simply want to monitor the transformations that are considered. An analysis pass can observe the results of other passes and collect statistics about their behavior.

###### Where does the pass need to go?
We need to inject a custom analysis pass into the pass manager pipeline. This pass would observe the IR before and after each transformation pass and log any changes or failures.
