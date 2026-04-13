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

![[Pasted image 20260413004821.png]]


**Polybench ADI**:
Figures:
- ![[Pasted image 20260413030245.png]]
	- Panel A: It shows RAJA’s hot loop is structurally more complex
		- RAJA presents a more fragmented hot loop
		- this may make recurrence optimization harder
	- Panel B: It directly supports the recurrence story
		- native preserves more loop-carried SSA structure
		- native has actual forwarded recurrence values
		- RAJA largely loses that forwarding
	- Caption: R evidence for the performance degradation of RAJA in Polybench ADI at -O1.
Panel (a) shows that RAJA introduces a more complex hot-loop CFG. Panel (b) shows that the native implementation preserves more loop-carried PHIs and forwarded values, indicating more effective register-level propagation of recurrence values. Panel (c) shows that RAJA correspondingly exhibits substantially higher load count, GEP count, and live SSA pressure, consistent with recurrence values being materialized through memory rather than forwarded through registers
Polybench ADI implements an Alternating Direction Implicit (ADI) method, a numerical scheme commonly used to solve partial differential equations such as diffusion problems. The computation consists of two sweeps—column-wise and row-wise—each performing forward and backward passes that resemble a tridiagonal solve. These sweeps introduce strong **loop-carried dependencies**, where values computed in one iteration (e.g., `p[i][j-1]`, `q[i][j-1]`, or `v[k+1][i]`) are immediately consumed in the next. As a result, the algorithm is inherently **recurrence-dominated**, and its efficient execution relies on keeping these recurrence values in registers and forwarding them across iterations rather than repeatedly accessing memory. This makes ADI a particularly sensitive benchmark for evaluating how well a compiler preserves and optimizes loop-carried data dependencies.

At a high level, we begin by examining aggregate structural and instruction-level IR metrics to understand whether the RAJA and native implementations differ in their overall representation (as shown in Figure X). Both versions exhibit comparable total loop cyclomatic complexity (`numLoopCyclomaticComplexity`), indicating a similar amount of control-flow structure across the program. However, moving to **maximum-based metrics** reveals a key distinction: the RAJA implementation has higher **function-level cyclomatic complexity** and increased **maximum loop and innermost-loop cyclomatic complexity** (`maxLoopCyclomaticComplexity`, `maxInnerLoopCyclomaticComplexity`). This suggests that RAJA concentrates more control-flow complexity within its most performance-critical regions. Consistent with this, the RAJA kernel exhibits higher **inner-loop basic blocks and branch instructions** (`maxInnerLoopBasicBlocks`, `maxInnerLoopBranchInsts`) and introduces **loop-invariant branches inside loops**, indicating a more fragmented control-flow structure in the hot path. In addition, RAJA shows increased **instruction count**, **GEP operations**, **load instructions**, and **live SSA values**, all of which point to greater pressure on memory and register resources compared to the native implementation.

Guided by these high-level observations, we then narrow the analysis to metrics that capture loop-carried dependencies and value propagation—critical for a recurrence-heavy kernel like ADI. Here, a clear divergence emerges. The native implementation exhibits a higher number of **loop-carried PHIs and forwarded values** (`numLoopCarriedPHIs`, `numLoopCarriedForwardedValues`, and their maxima), indicating that recurrence variables are efficiently propagated across iterations in SSA form and retained in registers. In contrast, the RAJA implementation shows reduced or absent forwarding behavior. This difference is directly reflected in the **inner-loop memory behavior**: the RAJA version has increased **inner-loop load counts** (`numInnerLoopLoads` and corresponding maxima), indicating that values that should be forwarded through PHIs are instead being repeatedly reloaded from memory. Given the structure of ADI, where each iteration depends on the immediate prior values, this inability to forward recurrence values forces the RAJA implementation to materialize these dependencies through memory accesses. Combined with elevated **GEP counts** and **live SSA pressure**, this suggests that the compiler is unable to maintain recurrence values in registers. The increased control-flow complexity in RAJA likely disrupts the compiler’s ability to recognize and optimize these recurrence patterns, preventing effective value forwarding. Consequently, the RAJA kernel incurs additional memory traffic and loses opportunities for register reuse, leading to degraded performance relative to the native implementation.

**Optimization Sensitive**:
- Apps_EDGE3D??
- Apps_MASS3DEA
- Apps_MASS3DPA
- Basic_INDEXLIST_3LOOP : Removed due to high variance

![[Screenshot_20260412_215052.png]]

![[Pasted image 20260413005058.png]]
![[Pasted image 20260413005109.png]]
![[Pasted image 20260413005127.png]]
