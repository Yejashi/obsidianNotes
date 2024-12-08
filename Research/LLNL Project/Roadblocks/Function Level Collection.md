Optimizations in LLVM are often modular, and specific passes might target different granularities of the IR. This means, that we can't just start the function level and go down.

### When the Discrepancy Can Occur
- A basic block-level pass (e.g., loop unrolling, constant folding) might be applied to one or more basic blocks without triggering a function-level pass. 
	- This can occur because LLVM's pass manager schedules and runs passes based on dependencies and optimization goals, and not every function must go through a function-level transformation before block-level optimizations.
- 