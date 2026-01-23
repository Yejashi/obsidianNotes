
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
			- ~12% percent change in favor of Base for all optsfor all opts
	- 