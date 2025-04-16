##### LICM
**LICM** stands for Loop Invariant Code Motion. It is an optimization pass that scans loops for instructions that compute the same value on every iteration (i.e. loop invariant computations) and moves those instructions outside the loop. This reduces redundant work inside the loop, which can lead to faster code execution and potentially simpler code for further optimizations.

##### Inlining
**Inlining** is a compiler optimization that replaces a function call with the actual body of the function at the call site. This eliminates the overhead of the call (such as saving registers and setting up a new stack frame) and exposes the function’s code to further optimizations like constant propagation and dead code elimination.

Note: There are different types of inlining: i.e partial inlining

