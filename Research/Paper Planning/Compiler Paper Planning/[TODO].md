
### Runtime Behaviors
#### RAJA vs Base
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

