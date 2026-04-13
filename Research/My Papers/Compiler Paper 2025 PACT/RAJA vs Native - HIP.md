![[Pasted image 20260412193845.png]]

![[Pasted image 20260412194907.png]]

**Optimization Agnostic**:
- Apps_CONVECTION3DPA ??
- Apps_DIFFUSION3DPA 
- Polybench_ADI
- Polybench_ATAX
- Polybench_GEMVER, Polybench_GEMM
- Polybench_MVT

![[Pasted image 20260412215925.png]]

**Polybench ADI**
At a high level, the IR metrics indicate that the RAJA and native implementations of Polybench ADI differ in both structural complexity and instruction behavior, with the RAJA version exhibiting a more complex and heavier-weight representation. While the total loop cyclomatic complexity is similar, the RAJA kernel shows higher function-level complexity and, more importantly, increased max loop and innermost-loop cyclomatic complexity. This is accompanied by a clear increase in basic blocks and branch instructions within the inner loop, as well as the presence of loop-invariant branches, all of which point to a more fragmented control-flow structure in the hot region. Beyond control flow, the RAJA version also incurs significantly higher instruction count, GEP operations, load instructions, and live SSA values, indicating greater pressure on both the memory system and register allocation. Taken together, these high-level metrics suggest that although both implementations perform the same computation, the RAJA version presents a more complex and less streamlined IR to the compiler, particularly in the performance-critical inner loops.

Narrowing down to the key difference, the loop-carried data dependencies reveal the underlying cause of this inefficiency. The native implementation exhibits a higher number of loop-carried PHIs and forwarded values, which indicates that recurrence variables are kept in registers and propagated directly across loop iterations. In contrast, the RAJA version shows a reduction—or complete absence—of such forwarding behavior, despite performing the same computation. This implies that the compiler is unable to maintain recurrence values in SSA form across iterations and instead must materialize them through memory via additional loads and address computations, as reflected in the elevated load and GEP counts. The increased control-flow complexity in RAJA likely interferes with the compiler’s ability to recognize and optimize these recurrence patterns, preventing effective value forwarding. As a result, the RAJA kernel relies more heavily on memory traffic rather than register reuse, leading to higher overhead and ultimately worse performance compared to the native implementation.

**Optimization Sensitive**:
- Apps_EDGE3D??
- Apps_MASS3DEA
- Apps_MASS3DPA
- Basic_INDEXLIST_3LOOP : Removed due to high variance

![[Screenshot_20260412_215052.png]]

