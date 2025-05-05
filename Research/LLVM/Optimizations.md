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

##### sdagisel

The **sdagisel** pass (short for _SelectionDAG Instruction Selection_) is a backend code generation pass that translates LLVM's intermediate representation (IR) into target-specific machine instructions. It works by lowering IR to a Selection Directed Acyclic Graph (SelectionDAG), which expresses operations and data dependencies in a form suited for pattern matching against the target's instruction set. By matching DAG nodes to patterns, `sdagisel` emits optimized machine instructions tailored for the target architecture. This pass is a key step in converting IR into executable machine code.

**Applied at:** This pass is active during **code generation** and runs at **all optimization levels, including -O0**, since instruction selection is necessary to produce machine code.

---

##### tailcallelim

The tail call elimination pass (**tailcallelim**) examines function calls that occur in tail position and transforms them into jumps instead of regular calls. By reusing the current function’s stack frame for the callee, it reduces call overhead and prevents the call stack from growing—especially beneficial for recursive functions.  
**Applied at:** Tail call elimination is typically performed starting at **-O1** and is enhanced at higher optimization levels like **-O2** and **-O3**.



## How optimizations vary
### Between -O2 and -O3

Both -O2 and -O3 enable a similar core set of optimizations. However, -O3 adjusts the same passes to be more aggressive in their application. Key differences include:

- **More Aggressive Inlining:**
    - At -O3, the threshold for inlining is increased. This means that larger or more complex functions are more likely to be inlined, potentially boosting performance even if the binary size grows.
- **Enhanced Loop Optimizations:**
    - -O3 relaxes the thresholds for loop transformations such as unrolling and vectorization. As a result, loops that might be left untouched or only minimally optimized at -O2 can be further optimized under -O3, sometimes resulting in faster execution at the cost of increased code size.
- **Additional Target-Specific and Interprocedural Optimizations:**
    
    - There are also extra target-specific tweaks and broader interprocedural optimizations enabled at -O3. These adjustments further refine the heuristics of the optimizations to extract more performance from the code.

---

### Between -O1 and -O2

The jump from -O1 to -O2 primarily involves the introduction of additional optimization passes and more aggressive tuning. The changes include:

- **Additional Loop Transformations:**
    
    - While -O1 applies basic loop optimizations, -O2 introduces more advanced techniques such as loop unrolling, loop unswitching, and in some cases, vectorization, which can enhance performance in compute-intensive loops.
        
- **Enhanced Inlining:**
    
    - Both levels perform inlining, but -O2 uses a more aggressive approach. More functions are inlined compared to -O1, contributing to improved runtime performance by reducing function call overhead.
        
- **More Extensive Global Optimizations:**
    
    - At -O2, the optimizer performs more comprehensive interprocedural and global analyses, such as advanced constant propagation and better dead code elimination. These optimizations improve the overall efficiency of the generated code.
        
- **Additional Target-Specific Tweaks:**
    
    - -O2 also enables extra target-specific optimizations that tailor the code generation more closely to the underlying hardware, further boosting performance beyond what is achieved at -O1.
        

---

### Summary

- **-O1** offers a balanced approach, applying basic optimizations with minimal impact on compile time.
    
- **-O2** builds on -O1 by adding more sophisticated optimizations—particularly for loops, inlining, and global code analysis—providing better performance while modestly increasing compile time and binary size.
    
- **-O3** pushes these optimizations further by relaxing thresholds and enabling extra aggressive passes, which can lead to even higher performance at the potential expense of longer compile times and larger binaries.
    

Each level is designed with different trade-offs in mind: **-O1** prioritizes compile speed and moderate performance improvements, **-O2** strikes a balance between performance and compile time, and **-O3** aims for maximum performance where binary size and compile time are less of a concern.