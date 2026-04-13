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
At a high level, we begin by examining aggregate structural and instruction-level IR metrics to understand whether the RAJA and native implementations differ in their overall representation. From this perspective, the two versions exhibit comparable total loop cyclomatic complexity (`numLoopCyclomaticComplexity`), suggesting a similar amount of control-flow structure across the program as a whole. However, a closer look at **maximum-based metrics** reveals an important distinction: the RAJA implementation has higher **function-level cyclomatic complexity** and increased **maximum loop and innermost-loop cyclomatic complexity** (`maxLoopCyclomaticComplexity`, `maxInnerLoopCyclomaticComplexity`). This indicates that RAJA concentrates more control-flow complexity in its most critical regions. Supporting this observation, the RAJA kernel also shows higher values for **inner-loop basic blocks and branch instructions** (`maxInnerLoopBasicBlocks`, `maxInnerLoopBranchInsts`), along with the presence of **loop-invariant branches inside loops**, pointing to a more fragmented and less streamlined control-flow structure in the hot path. Complementing these structural differences, the RAJA version exhibits substantially higher **instruction count**, **GEP operations**, **load instructions**, and **live SSA values**, which collectively suggest increased pressure on both memory and register resources.

Guided by these high-level observations, we then narrow our analysis to metrics that capture loop-carried dependencies and value propagation. Here, a clear divergence emerges: the native implementation demonstrates a higher number of **loop-carried PHIs and forwarded values** (`numLoopCarriedPHIs`, `numLoopCarriedForwardedValues`, and their corresponding maxima), indicating that recurrence variables are efficiently propagated across loop iterations in SSA form and retained in registers. In contrast, the RAJA implementation exhibits reduced or absent forwarding behavior, despite performing the same computation. This lack of forwarding, combined with the elevated **load counts**, **address computations (GEPs)**, and **live SSA pressure**, indicates that recurrence values are instead being repeatedly materialized from memory. The increased control-flow complexity observed earlier likely disrupts the compiler’s ability to recognize and optimize these recurrence patterns, preventing effective value forwarding. Consequently, the RAJA kernel incurs additional memory traffic and loses opportunities for register reuse, leading to degraded performance relative to the native implementation

**Optimization Sensitive**:
- Apps_EDGE3D??
- Apps_MASS3DEA
- Apps_MASS3DPA
- Basic_INDEXLIST_3LOOP : Removed due to high variance

![[Screenshot_20260412_215052.png]]

