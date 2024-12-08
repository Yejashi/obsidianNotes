Optimizations in LLVM are often modular, and specific passes might target different granularities of the IR. This means, that we can't just start the function level and go down.

### When the Discrepancy Can Occur
- A basic block-level pass (e.g., loop unrolling, constant folding) might be applied to one or more basic blocks without triggering a function-level pass. 
	- This can occur because LLVM's pass manager schedules and runs passes based on dependencies and optimization goals, and not every function must go through a function-level transformation before block-level optimizations.
- Similarly, an analysis pass might collect data at the basic block level but never directly analyze the function as a whole.

### Implications for Data Collection
If we only collect function-level passes, we may miss optimizations applied to its basic blocks. To fully capture all optimizations involving a function, we must:

**Track Passes at Multiple Levels:**
- Record function passes for the overall function.
- Record basic block passes for each basic block within the function.
- Consider instruction-level passes, if needed

**Aggregate the Data:**
- When reporting the optimization details for a function, we combine data from all levels (function, basic block, instruction) to provide a complete picture.

### Example
Function `foo`:
- No function-level passes are applied.
- Basic block `BB1` within `foo` has a loop unrolling optimization applied.
- Basic block `BB2` within `foo` has constant folding applied.


