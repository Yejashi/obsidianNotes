##### LICM
**LICM** stands for Loop Invariant Code Motion. It is an optimization pass that scans loops for instructions that compute the same value on every iteration (i.e. loop invariant computations) and moves those instructions outside the loop. This reduces redundant work inside the loop, which can lead to faster code execution and potentially simpler code for further optimizations.

##### Inlining
**Inlining** is a compiler optimization that replaces a function call with the actual body of the function at the call site. This eliminates the overhead of the call (such as saving registers and setting up a new stack frame) and exposes the function’s code to further optimizations like constant propagation and dead code elimination.

Note: There are different types of inlining: i.e partial inlining

##### loop-vectorize
The **loop-vectorize** pass in LLVM automatically transforms a loop so that several iterations can be executed in parallel using SIMD instructions. It does this by analyzing the loop to ensure that it’s safe to combine iterations, then rewrites the loop body to operate on vector types (loading/storing multiple values at once) and adjusts the loop’s induction variable to increment by the vector width rather than one.

##### loop-idiom
The **loop idiom** recognition pass in LLVM examines loops to see if they match common, well‑known patterns—such as loops performing a memory copy, a memory set, or simple arithmetic accumulation—and then replaces them with more efficient, specialized intrinsics or library calls.

##### regalloc
Register allocation (abbreviated as "**regalloc**") is the compiler phase responsible for mapping the program’s virtual registers—which can be arbitrarily many in the intermediate representation—to a limited number of physical registers available on the target machine. This pass must decide which values remain in registers and which are temporarily stored (spilled) to memory when registers are scarce. An efficient register allocator minimizes the costly memory accesses and helps generate faster code, often using algorithms such as graph-coloring or linear scan to perform this mapping.

##### slp-vectorizer
The SLP (Superword Level Parallelism) vectorizer is an LLVM optimization pass that identifies groups of independent scalar operations within a basic block that perform the same computation and can be executed in parallel. It then packs these operations into a single SIMD (Single Instruction, Multiple Data) instruction, effectively reducing the instruction count and improving data throughput. This approach is particularly effective for optimizing loops or blocks of code where the same operation is applied to multiple data elements.

##### gvn
Global Value Numbering (**GVN**) is an optimization pass that identifies and eliminates redundant computations across a function. It works by assigning “value numbers” to computations; if two computations yield the same value, one of them can be replaced with the other. This not only removes duplicate work but also exposes opportunities for further optimizations like constant propagation and dead code elimination.

##### loop-unrolling
**Loop unrolling** is an optimization that replicates the loop body multiple times to reduce the overhead associated with loop control (like incrementing and branch checking). By doing this, fewer iterations are needed, and the loop’s control logic is executed less frequently. This transformation can expose opportunities for further optimizations such as vectorization or improved instruction scheduling, but it may also lead to increased code size if overused.

##### TTI
**TTI** (Target Transform Info) is an LLVM interface that supplies target-specific cost information to optimization passes. It allows these passes to query details about the target’s architecture—such as the cost of arithmetic operations, memory access penalties, or vectorization capabilities—so that they can make informed decisions about which transformations will improve performance on that specific hardware. This enables the compiler to tailor optimizations like inlining, loop transformations, or vectorization based on the target’s characteristics.

##### tailcallelim
The tail call elimination pass in LLVM examines function calls that occur as the last operation (i.e. in tail position) and transforms them into jumps instead of regular calls. By reusing the current function’s stack frame for the tail-called function, this optimization reduces call overhead and prevents the growth of the call stack—which is particularly beneficial for recursive functions.