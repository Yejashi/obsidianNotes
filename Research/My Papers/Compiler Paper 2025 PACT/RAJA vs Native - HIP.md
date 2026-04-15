![[Pasted image 20260412193845.png]]

![[Pasted image 20260412194907.png]]

To understand the structural origins of the runtime differences observed between Native HIP and RAJA HIP, we perform a static analysis of the LLVM IR generated for each variant. We begin by identifying all kernels whose runtime percent difference between Native and RAJA is statistically significant across all three optimization levels (O1, O2, O3). From these, we partition the kernels into two categories based on how the performance gap responds to optimization level:
- **Optimization-Agnostic**: Kernels where the relative performance difference between Native and RAJA remains stable across O1, O2, and O3. The optimizer neither closes nor widens the gap — the structural cause of the difference is baked into the IR in a way that survives all optimization passes
- **Optimization-Sensitive**: Kernels where the performance gap changes meaningfully across optimization levels, indicating that the optimizer is able to partially resolve (or exacerbate) the structural differences between the two variants

**Optimization Agnostic**:
- Apps_CONVECTION3DPA ??
- Apps_DIFFUSION3DPA 
- Polybench_ADI
- Polybench_ATAX
- Polybench_GEMVER, Polybench_GEMM
- Polybench_MVT

![[Pasted image 20260412215925.png]]
![[Pasted image 20260414041633.png]]

Optimization Agnostic Kernels:
We select seven optimization agnostic kernels that span three distinct behavioral categorios observed at runtime:
- RAJA Favorable (RAJA faster than Native): Apps_CONVECTION3DPA and Apps_DIFFUSION3DPA, where RAJA achieved 5-10% speedups across all optimization levels.
- RAJA unfavorable (RAJA substantially slower): Polybench_ADI, Polybench_ATAX, Polybench_GEMVER, Polybench_MVT, where RAJA inclurs 13-54% overhead that persists across all optimization levels.
- Near-Parity: Polybench_GESUMMV, where RAJA matches Native within 1% despite exhibiting structural characteristics similar to the unfavoral group (polybench)
The inclusion of Polybench_GESUMMV is deliberate: it serves as a control case allowing us distinguish which static IR features correlate with runtime degradation from those that are merely present in RAJA generated code but do not manifest as performance loss.

The selected subset serves three complementary purposes. First, `Apps_CONVECTION3DPA` and `Apps_DIFFUSION3DPA` represent favorable abstraction cases in which RAJA achieves better runtime performance than Native, allowing us to study compiler-visible structure associated with benign or advantageous abstraction. Second, the PolyBench kernels with substantial RAJA slowdowns represent abstraction-sensitive cases in which semantically equivalent implementations diverge in performance. Third, `Polybench_GESUMMV` is included despite near-runtime parity because it provides an important control: if its static characteristics resemble those of the slower PolyBench kernels, then structural divergence alone is insufficient to explain performance loss.


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

**Polybench_ATAX, POlybench_GEMVER, Polybench_MVT**:
![[Pasted image 20260413063136.png]]
Polybench_ATAX, Polybench_GEMVER, Polybench_MVT, and Polybench_GESUMMV are dense linear algebra kernels from the PolyBench suite that consist primarily of matrix-vector products and rank-update operations. Despite differences in composition—ATAX performing two matrix-vector phases, MVT executing both row-wise and transposed matrix-vector products, GEMVER combining a rank-2 update with multiple dot products and vector updates, and GESUMMV computing a weighted sum of two matrix-vector products—all four share the same essential computational structure: deeply nested loops, regular affine indexing, and simple accumulation patterns. Because of this regularity, these kernels are especially sensitive to how cleanly the compiler can represent loop nests, induction variables, and accumulation state in the IR. In the best case, they compile into compact, canonical inner loops with minimal control flow and a small amount of loop-carried state, which makes them ideal for studying whether an abstraction preserves or obscures optimization-friendly structure.

Figure X shows that the RAJA implementations of all four kernels are consistently more structurally complex than their Native counterparts along three related dimensions. In the left panel, RAJA increases loop-carried state across all kernels, with higher values for loop-carried PHIs and other loop-carried PHIs (M1–M3), indicating that more SSA state is threaded through the loop than in the Native versions. The center panel shows that this added state is accompanied by greater inner-loop fragmentation: RAJA consistently raises the maximum number of inner-loop branches, PHIs, and basic blocks (M4–M6), meaning that the hot loop body is less compact and more fragmented. The right panel shows that this fragmentation also manifests as less canonical loop structure, with higher maximum inner-loop cyclomatic complexity, more loop-invariant branches inside loops, and higher total inner-loop cyclomatic complexity (M7–M9). Together, these results indicate that RAJA preserves the same underlying computation but expresses it through more elaborate loop control and state management.

However, the fourth panel reveals a key distinction that explains the observed performance behavior. While ATAX, GEMVER, and MVT exhibit not only increased structural complexity but also changes in hot-loop work—specifically increases in integer arithmetic and, in some cases, memory-related operations (M10–M12)—GESUMMV does not. Despite experiencing similar increases in control-flow complexity, GESUMMV preserves nearly identical hot-loop arithmetic and memory behavior between RAJA and Native. This indicates that the additional abstraction-induced structure in GESUMMV remains largely outside the critical execution path or does not perturb the core loop body in a way that affects execution efficiency.

As a result, ATAX, GEMVER, and MVT show meaningful performance degradations because abstraction increases both control-flow complexity and the amount of work performed within the hot loop, directly impacting throughput. In contrast, GESUMMV demonstrates that increased structural complexity alone is insufficient to cause performance loss: only when this complexity translates into additional work or disrupts the canonical structure of the hot loop does it degrade performance. This distinction refines the earlier conclusion—performance degradation is not driven purely by abstraction-induced structural overhead, but by whether that overhead materially alters the computational or memory behavior of the inner loop.

How does the fix resolve this?
- We were correct because the specific structural problems identified in Figure X are exactly the ones that disappear in the fixed MVT RAJA IR, and the performance difference disappears with them.
- In our explanation, we argued that the slower RAJA versions of ATAX, GEMVER, and MVT were not doing more useful arithmetic, but were instead expressing the same computation through more elaborate loop control and state management. The figure made that precise in three ways: more loop-carried state (M1–M3), more inner-loop fragmentation (M4–M6), and more non-canonical loop structure (M7–M9). When we compare the old slow RAJA MVT IR against Native, that is exactly what we see: the accumulation is carried through multiple PHIs rather than a single clean accumulator, the inner computation is split across extra executor/lambda blocks, and the hot loop contains more control-flow joins and continuations than the compact Native reduction loop. By contrast, in the fixed RAJA MVT IR, the hot loop collapses into a much more Native-like canonical form: one induction PHI, one accumulator PHI, two loads, one multiply, one add, one increment, one exit compare, and one backedge branch. That directly reflects a reduction in the very phenomena highlighted by the figure—less loop-carried state, less fragmentation, and a more canonical loop body.
- More concretely, the old slow RAJA MVT carried the dot-product state through several accumulator-like PHIs and multiple executor continuation blocks before the final store, whereas the fixed RAJA version carries the accumulation through a single inner-loop accumulator PHI and exits cleanly into one store block, just like Native. The old version also inserted an extra conditional split around the effective inner-loop body, while the fixed version restores the compact reduction structure that our explanation said these regular PolyBench kernels benefit from. That is why the validation is strong: the performance recovers when the loop becomes structurally simpler in exactly the dimensions we claimed were problematic. So our conclusion was not just plausible in the abstract; it made a testable prediction, and the fixed MVT kernel behaves exactly as that prediction would suggest.


**Optimization Sensitive**:
- Apps_EDGE3D??
- Apps_MASS3DEA
- Apps_MASS3DPA
- Basic_INDEXLIST_3LOOP : Removed due to high variance

![[Screenshot_20260412_215052.png]]

![[Pasted image 20260413005058.png]]
![[Pasted image 20260413005109.png]]
![[Pasted image 20260413005127.png]]
