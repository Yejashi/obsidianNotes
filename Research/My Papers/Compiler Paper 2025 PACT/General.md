Experimental Search Space
- Programming models: Native, RAJA
- Target Backends: HIP, OpenMP
- Total Node Problem Sizes: 8M, 32M, 128M
- Optimization Levels: O1, O2, O3

Execution Configuration
- System: LLNL Tuolumne
- Compiler: ROCm 6.4.0
- 20 runs per configuration
- OpenMP Configuration
	- RAJAPerf Variants:  RAJA_OpenMP, Base_OpenMP
	- Number of  ranks: 1
	- Number of cores per rank: 84
	- Number of threads: 84
	- Per rank problem sizes: 8M, 32M, 128M
- HIP Configuration
	- RAJAPerf Variants: RAJA_HIP, Base_HIP
	- Number of ranks: 4
	- Number of GPUs per rank: 1
	- Per rank problem sizes: 2M, 8M, 32M

Variance: 
