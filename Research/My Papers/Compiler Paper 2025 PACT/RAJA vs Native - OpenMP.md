![[Pasted image 20260412193904.png]]
![[Pasted image 20260412194926.png]]
Kernels to Analyze:
- Apps_MEMSET
- Apps_FIR
- Apps_LTIMES, Apps_LTIMES_NO_VIEW
- Basic_IF_QUAD
- Basic_INIT_VIEW1D, Basic_INIT_VIEW1D_OFFSET
- Basic_NEWSTED_INIT

From the full set of OpenMP kernels, we select a subset that exhibits representative performance divergence patterns between RAJA and native implementations. We focus on kernels that (1) show consistent and statistically stable differences, (2) expose sensitivity to abstraction or indexing structure, and (3) allow controlled comparisons between semantically equivalent implementations.

In particular, we include paired kernels such as _Apps_LTIMES_ and _Apps_LTIMES_NO_VIEW_, which differ primarily in their use of RAJA Views, and _Basic_INIT_VIEW1D_ and _Basic_INIT_VIEW1D_OFFSET_, which differ only in indexing structure. These pairs enable isolation of abstraction-induced and indexing-induced effects on compiler optimization. We also include representative kernels such as _Apps_FIR_ and _Basic_NESTED_INIT_ that exhibit large or optimization-sensitive divergence.

Kernels with high run-to-run variance are excluded to ensure that observed differences are stable and attributable to structural effects rather than measurement noise.

![[Pasted image 20260414095729.png]]

**Apps_MEMSET**
**Apps_**
