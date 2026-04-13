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
At a high level, we begin by examining aggregate structural and instruction-level IR metrics to understand whether the RAJA and native implementations differ in their overall representation (as shown in Figure X). From this perspective, both versions exhibit comparable total loop cyclomatic complexity (`numLoopCyclomaticComplexity`), suggesting a similar amount of control-flow structure across the program as a whole. However, moving beyond aggregate metrics to **maximum-based measures** reveals a key distinction: the RAJA implementation has higher **function-level cyclomatic complexity** and increased **maximum loop and innermost-loop cyclomatic complexity** (`maxLoopCyclomaticComplexity`, `maxInnerLoopCyclomaticComplexity`). This indicates that RAJA concentrates more control-flow complexity within its most critical regions. Consistent with this, the RAJA kernel also shows higher values for **inner-loop basic blocks and branch instructions** (`maxInnerLoopBasicBlocks`, `maxInnerLoopBranchInsts`), as well as the presence of **loop-invariant branches inside loops**, pointing to a more fragmented control-flow structure in the hot path. In addition to these structural differences, the RAJA version exhibits higher **instruction count**, **GEP operations**, **load instructions**, and **live SSA values**, all of which suggest increased pressure on both memory and register resources compared to the native implementation.

Guided by these high-level observations, we then narrow our analysis to metrics that capture loop-carried dependencies and value propagation. Here, a clear divergence emerges. The native implementation demonstrates a higher number of **loop-carried PHIs and forwarded values** (`numLoopCarriedPHIs`, `numLoopCarriedForwardedValues`, and their maxima), indicating that recurrence variables are propagated efficiently across iterations in SSA form and retained in registers. In contrast, the RAJA implementation exhibits reduced or absent forwarding behavior, despite performing the same computation. This difference is directly reflected in the **inner-loop memory behavior**: the RAJA version has increased **inner-loop load counts** (`numInnerLoopLoads` and corresponding maxima), indicating that values that would otherwise be forwarded through PHIs are instead being repeatedly reloaded from memory. Together with the elevated **GEP counts** and **live SSA pressure**, this suggests that the compiler is unable to maintain recurrence values in registers and must materialize them through memory accesses. The increased control-flow complexity in RAJA likely disrupts the compiler’s ability to recognize and optimize these recurrence patterns, preventing effective value forwarding. As a result, the RAJA kernel incurs additional memory traffic and loses opportunities for register reuse, leading to degraded performance relative to the native implementation.

**Optimization Sensitive**:
- Apps_EDGE3D??
- Apps_MASS3DEA
- Apps_MASS3DPA
- Basic_INDEXLIST_3LOOP : Removed due to high variance

![[Screenshot_20260412_215052.png]]

