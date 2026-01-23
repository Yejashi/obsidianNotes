## Analysis of Divergent Kernels


| Kernel              | % Change         |
| ------------------- | ---------------- |
| Apps_MASS3DEA       | 0%, 1247%, 1349% |
| Polybench_ADI       |                  |
| Polybench_ATAX      |                  |
| Polybench_MVT       |                  |
| Polybench_GEMVER    |                  |
| Apps_DIFFUSION3DPA  |                  |
| Apps_EDGE3D         |                  |
| Apps_CONVECTION3DPA |                  |

### Runtime Behaviors
- Majority of kernels show minimal change in performance (~0-3%)
- Exceptions:
	- In favor of Base
		- Apps_MASS3DEA
			- Parity at -O1 and ~1247% 
		- Polybench_ADI
			- ~22% for all opts
		- Polybench_ATAX
			- ~12% for all opts
		- Polybench_MVT
			- ~10% for all opts
		- Polybench_GEMVER
			- ~7% for all opts
	- In favor of RAJA
		- Apps_DIFFUSION3DPA
			- ~17-20% for all opts
		- Apps_EDGE3D
			- ~7% for -O1 and parity for -O2 and -O3
		- Apps_CONVECTION3DPA
			- ~7% for all opts

### TODO: Control Flow
- Majority of kernels show significant changes in number of instructions
- Divergent kernels from runtime (Base)
	- Apps_MASS3DEA
		- 16% percent  more instructions in Base