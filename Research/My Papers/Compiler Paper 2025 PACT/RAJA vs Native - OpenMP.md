![[Pasted image 20260412193904.png]]
![[Pasted image 20260412194926.png]]
Kernels to Analyze:
- Apps_MEMSET
- Apps_FIR
- Apps_LTIMES, Apps_LTIMES_NO_VIEW
- Basic_IF_QUAD
- Basic_INIT_VIEW1D, Basic_INIT_VIEW1D_OFFSET
- Basic_NEWSTED_INIT

From the full set of OpenMP kernels, we select a representative subset for detailed static analysis based on two criteria: (1) consistency of performance differences across optimization levels and (2) statistical stability (low run-to-run variance). Kernels exhibiting high variance, such as Basic_MAT_MAT_SHARED and Basic_ARRAY_OF_PTRS, are excluded to avoid confounding effects.

The selected kernels span three behavioral categories: (i) consistently large slowdowns (Apps_FIR, Apps_LTIMES), (ii) optimization-sensitive behavior where performance changes across compiler optimization levels (Basic_INIT_VIEW1D, Basic_INIT_VIEW1D_OFFSET, Basic_NESTED_INIT), and (iii) moderate but stable differences (Algorithm_MEMSET, Polybench_3MM). This selection enables us to study both steady and compiler-dependent divergence patterns between RAJA and native implementations.
![[Pasted image 20260412225221.png]]
![[Pasted image 20260412225225.png]]
![[Pasted image 20260412225229.png]]

