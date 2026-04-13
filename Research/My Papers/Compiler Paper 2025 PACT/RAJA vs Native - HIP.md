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
	- Caption: IR evidence for the performance degradation of RAJA in Polybench ADI at -O1. Panel (a) shows that RAJA introduces a more complex hot-loop CFG. Panel (b) shows that the native implementation preserves more loop-carried PHIs and forwarded values, indicating more effective register-level propagation of recurrence values. Panel (c) shows that RAJA correspondingly exhibits substantially higher load count, GEP count, and live SSA pressure, consistent with recurrence values being materialized through memory rather than forwarded through registers
Polybench ADI implements an Alternating Direction Implicit (ADI) method, a numerical scheme used to solve partial differential equations such as diffusion problems. The computation consists of two sweeps—column-wise and row-wise—each performing forward and backward passes that resemble tridiagonal solves. These passes introduce strong loop-carried dependencies, where values computed in one iteration (e.g.,  $p[i][j−1],  q[i][j−1], or   v[k+1][i])$ are immediately consumed in the next. As a result, ADI is inherently recurrence-dominated, and efficient execution depends on the compiler’s ability to retain these recurrence values in registers and propagate them across iterations via SSA-based forwarding rather than repeatedly reloading them from memory. This makes ADI a particularly sensitive benchmark for evaluating how well compilers preserve and optimize loop-carried dependencies.

We begin by examining high-level structural IR metrics to understand how the RAJA and native implementations differ in their representation (Figure X, left). While both implementations encode the same algorithm, the RAJA version exhibits consistently higher inner-loop control-flow complexity, with increases in maximum inner-loop cyclomatic complexity, basic blocks, and branch instructions (e.g., 3 vs. 2 for cyclomatic complexity, and 3 vs. 1 for both basic blocks and branches). These differences indicate that the RAJA kernel introduces a more fragmented control-flow structure within the hot loop. Such structural complexity can obscure canonical loop forms and make it more difficult for the compiler to recognize recurrence patterns and apply loop optimizations that rely on them.

We then focus on metrics that capture recurrence structure and value propagation (Figure X, center). The native implementation exhibits both a higher number of loop-carried PHIs and, critically, non-zero forwarding PHIs and loop-carried forwarded values, indicating that recurrence variables are preserved in SSA form and actively propagated across iterations. In contrast, the RAJA implementation shows both reduced loop-carried PHIs and no forwarding behavior (all forwarding-related metrics equal to zero). This combination suggests not only that forwarding is absent, but that the underlying recurrence structure is less clearly represented in the IR, limiting the compiler’s ability to exploit it. Thus, while both implementations perform the same computation, only the native version exposes and leverages recurrence patterns in a way that enables effective register-based value propagation.

Finally, we examine the consequences of this difference (Figure X, right). The RAJA implementation shows a substantial increase in memory and address-generation activity, with significantly higher load instructions (85 vs. 31), GEP instructions (113 vs. 70), and live SSA values (18 vs. 12). Here, GEP (GetElementPtr) instructions represent address computations for memory accesses, so their increase reflects more complex or frequent indexing operations. Together, these metrics indicate that values which could otherwise be retained and reused in registers are instead recomputed or repeatedly loaded from memory, increasing both register pressure and memory traffic. In the context of ADI’s recurrence-heavy computation, this pattern is consistent with the loss of forwarding observed earlier: the additional control-flow complexity in RAJA likely prevents the compiler from recognizing recurrence relationships, resulting in missed opportunities for register reuse and increased reliance on memory accesses. This behavior aligns with the observed performance degradation of the RAJA implementation relative to the native version.

**Optimization Sensitive**:
- Apps_EDGE3D??
- Apps_MASS3DEA
- Apps_MASS3DPA
- Basic_INDEXLIST_3LOOP : Removed due to high variance

![[Screenshot_20260412_215052.png]]

![[Pasted image 20260413005058.png]]
![[Pasted image 20260413005109.png]]
![[Pasted image 20260413005127.png]]
