`__launch_bounds__` tells the compiler what block size you _promise_ to use when launching the kernel, so it can make better register and unrolling decisions.

It does **not** change how many threads actually run.  
It **changes how aggressively the compiler uses registers and unrolls code**.

This does **not** mean:
- The compiler changes how many threads are launched at runtime 
- The compiler magically knows the launch configuration

It does mean:
- The compiler is being given constraints about the launch configuration so it can make safer backend decisions, especially about registers, unrolling, and spilling.

The semantics of `__launch_bounds__`:
```
__global__ __launch_bounds__(MAX_THREADS_PER_BLOCK,
                            MIN_BLOCKS_PER_CU)
void kernel(...) { ... }
```

`MAX_THREADS_PER_BLOCK
- Means the kernel will never be launched with more than this many threads per block

As such, the compiler can assume:
- Maximum waves per block
- Maximum registers consumed per block


`MIN_BLOCKS_PER_CU`
- Tells the compiler to ensure that this many blocks can reside on each CU

This is a hard occupancy constraint.

From this, the compiler derives:
- A minimum number of waves per CU
- Which implies a maximum register budget per thread

The key idea is that `__launch_bounds_` turns occupancy from a soft heuristic into a hard constraint.
- Without it LLVM optimizes mostly for ILP
	- Occupancy is considered but loosely
- With it, LLVM must respect a register ceiling
	- Otherwise it would violate the requested occupancy


### How is this related to the loop-unroll pass?

Loop unrolling happens before register allocation, but:
- It uses TargetTransformInfo (TTI)
- Which already knows register pressure limits
- Which are affected by `__launch_bounds__`

So unrolling decisions are **constrained by future register pressure**, even though RA hasn’t run yet.