##### LICM

**LICM** stands for Loop Invariant Code Motion. It is an optimization pass that scans loops for instructions that compute the same value on every iteration (i.e. loop invariant computations) and moves those instructions outside the loop. This reduces redundant work inside the loop, which can lead to faster code execution and potentially simpler code for further optimizations.  
**Applied at:** Enabled starting at **-O1** (and used in all higher levels such as -O2 and -O3).

---

##### Inlining

**Inlining** is a compiler optimization that replaces a function call with the actual body of the function at the call site. This eliminates the overhead of the call (such as saving registers and setting up a new stack frame) and exposes the function’s code to further optimizations like constant propagation and dead code elimination. (Note: There are different types of inlining; for example, always_inline functions are inlined regardless of the optimization level.)  
**Applied at:** Basic inlining is typically enabled from **-O1** onward, with more aggressive inlining at **-O2** and **-O3** (and further tuned by options like -Ofast).

---

##### loop-vectorize

The **loop-vectorize** pass in LLVM automatically transforms a loop so that several iterations can be executed in parallel using SIMD instructions. It does this by analyzing the loop to ensure that it’s safe to combine iterations, then rewrites the loop body to operate on vector types (loading/storing multiple values at once) and adjusts the loop’s induction variable accordingly.  
**Applied at:** This pass is generally enabled at **-O2** and higher (including -O3 and -Ofast).

---

##### loop-idiom

The **loop idiom** recognition pass in LLVM examines loops to see if they match common, well‑known patterns—such as loops performing a memory copy, a memory set, or simple arithmetic accumulation—and then replaces them with more efficient, specialized intrinsics or library calls.  
**Applied at:** Typically enabled starting at **-O1** and continuing through **-O2** and **-O3**.

---

##### regalloc

Register allocation (abbreviated as **regalloc**) is the compiler phase responsible for mapping the program’s virtual registers (which are plentiful in LLVM’s IR) to the limited physical registers available on the target machine. It determines which values remain in registers and which must be spilled to memory when registers are scarce.  
**Applied at:** This phase occurs during code generation in every build – it is active even at **-O0**, though the quality and aggressiveness of the allocation improve at **-O1** and above.

---

##### slp-vectorizer

The SLP (Superword Level Parallelism) vectorizer is an LLVM optimization pass that identifies groups of independent scalar operations within a basic block that perform the same computation and can be executed in parallel. It then packs these operations into a single SIMD instruction, reducing the instruction count and improving throughput.  
**Applied at:** This pass is generally enabled at **-O2** and higher (including -O3).

---

##### gvn

Global Value Numbering (**GVN**) is an optimization pass that identifies and eliminates redundant computations across a function. It assigns “value numbers” to computations so that if two computations yield the same value, one can be replaced with the other. This not only removes duplicate work but also exposes further opportunities for optimizations like constant propagation and dead code elimination.  
**Applied at:** GVN is typically enabled starting at **-O1** and is used throughout **-O2** and **-O3**.

---

##### loop-unrolling

**Loop unrolling** is an optimization that replicates the loop body multiple times to reduce the overhead associated with loop control (such as incrementing and branch checking). Fewer iterations mean less loop control overhead and can expose further opportunities like vectorization or better scheduling. However, over-aggressive unrolling may increase code size.  
**Applied at:** Basic unrolling may occur at **-O1**, but more aggressive unrolling is typically enabled at **-O2** and **-O3** (and further tuned via flags like -funroll-loops).

---

##### TTI

**TTI** (Target Transform Info) is an LLVM interface that supplies target-specific cost information (such as the cost of arithmetic operations, memory accesses, and vector operations) to various optimization passes. This helps the compiler decide which transformations will yield performance gains on the specific hardware target.  
**Applied at:** TTI is used by nearly all optimizations in **-O1** and higher, guiding decisions across the optimization pipeline.

---

##### tailcallelim

The tail call elimination pass (**tailcallelim**) examines function calls that occur in tail position and transforms them into jumps instead of regular calls. By reusing the current function’s stack frame for the callee, it reduces call overhead and prevents the call stack from growing—especially beneficial for recursive functions.  
**Applied at:** Tail call elimination is typically performed starting at **-O1** and is enhanced at higher optimization levels like **-O2** and **-O3**.



## How optimizations vary
