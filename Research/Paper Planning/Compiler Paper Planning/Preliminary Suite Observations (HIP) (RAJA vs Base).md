## Analysis of Divergent Kernels


| Kernel              | Time % Change    | NumInsts % Change  | numBasicBlocks % Change |
| ------------------- | ---------------- | ------------------ | ----------------------- |
| Apps_MASS3DEA       | 0%, 1247%, 1349% | -16%, 2151%, 2151% | -10%, -17%, -17%        |
| Polybench_ADI       | 22%, 23%, 22%    | 17%, 17%, 17%      |                         |
| Polybench_ATAX      | 12%, 12%, 12%    | 110%, 133%, 133%   |                         |
| Polybench_MVT       | 10%, 9%, 9%      | 87%, 107%, 107%    |                         |
| Polybench_GEMVER    | 7%, 7%, 7%       | 82%, 92%, 92%      |                         |
| Apps_DIFFUSION3DPA  | -17%, -20%, -20% | -33%, -23%, -23%   |                         |
| Apps_EDGE3D         | -7%, -2%, -1%    | 7%, 2%, 2%         |                         |
| Apps_CONVECTION3DPA | -7%, -7%, -7%    | -38%, -32%, -32%   |                         |

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