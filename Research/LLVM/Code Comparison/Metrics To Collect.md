```
Steps

1. [ Clang / hipcc ]

2. [ IR metrics pass / remarks extraction pass ]  -> JSON[remarks, IR metrics] per func

3. [ Object / binary ]

4. [ LLVM-based binary analysis tool ] -> JSON[VGPR, SGPR, spills, occupancy]

```
#### Middle-End
Description
- An LLVM IR pass plugin that analyzes the IR and collects metrics, per function, which are dumped per module/TU to a json file.

Metrics:
1. Number of Loops
2. Max loop depth
3. Number of Basic blocks
4. Number of Branches
5. Number of Function calls
6. Total instruction count
7. Arithmetic instruction count
8. Memory instruction count
9. Number of PHI instructions
10. Number of Loop-invariant instructions
11. Number of Constant-trip loops
12. Avg instructions per BB
13. Max live SSA values
14. Number of GEP instructions
15. Loads/stores inside loops


What  the output will look like:
```
{
  "module": "MASS3DEA-Hip.cpp.o",
  "functions": [
    "_ZN8rajaperf4apps8Mass3DEAILm64EEEvPdS2_S2_": {
      "num_loops": 9,
      "max_loop_depth": 5,
      "num_basic_blocks": 42,
      "num_branches": 31,
      "num_calls": 0,
      "total_instructions": 1832,
      "arith_instructions": 624,
      "mem_instructions": 517,
      "num_phi": 211,
      "loop_invariant_insts": 143,
      "constant_trip_loops": 6,
      "avg_insts_per_bb": 43.6,
      "max_live_ssa": 128,
      "num_gep": 392,
      "loop_load_store": 401
    }
  ]
}
```

#### Post Compilation
Description:
- A post-codegen, static binary analysis tool that extracts kernel-level resource usage and ISA properties using LLVM’s object + AMDGPU libraries

Metrics:
- Kernel Resource
	1. VGPRs per thread
	2. SGPRs per thread
	3. Scratch bytes per thread
	4. LDS bytes per workgroup
- Derived Occupancy
	1. Max waves per CU
	2. Max threads per CU
- Instruction Level
	1. Total machine instruction count
	2. Machine load instruction count
	3. Machine store instruction count
	4. Private-memory (scratch) load/store count
	5. ALU vs memory instruction ratio


The necessary libraries:

| Tool                   | Backing library               |
| ---------------------- | ----------------------------- |
| `llvm-readobj`         | `llvm::object`                |
| `llvm-objdump`         | `llvm::object` + `llvm::MC`   |
| AMDGPU kernel metadata | `llvm::AMDGPU`                |
| Code object parsing    | `llvm::object::ELFObjectFile` |

How would this function?
A **standalone analysis tool** (linked against LLVM) that:
1. Loads the `.o` / `.hsaco` / binary
2. Parses AMDGPU kernel metadata
3. Optionally disassembles kernels
4. Emits structured JSON


What the output will look like:
```
{
  "functions": [
	  "_ZN8rajaperf4apps8Mass3DEAILm64EEEvPdS2_S2_" : {
		// Resources
	    "vgprs_per_thread": 128,
	    "sgprs_per_thread": 64,
	    "scratch_bytes_per_thread": 256,
	    "lds_bytes_per_workgroup": 0,
	    "wavefront_size": 64,
	    "workgroup_size": 256
		// Occupancy
	    "max_waves_per_cu": 2,
	    "max_threads_per_cu": 128,
		// ISA metrics
	    "total_instructions": 4120,
	    "alu_instructions": 1850,
	    "load_instructions": 1210,
	    "store_instructions": 940,
	    "scratch_load_store": 312
	  }
  ]
}
```

#### MISC
Analysis Remarks:
```
hipcc your_kernel.cpp -O3 -Rpass-analysis=kernel-resource-usage
```

```
remark: kernel-resource-usage: KernelName VGPRs: 64, SGPRs: 24, ScratchSize: 0, VGPRSpills: 0, SGPRSpills: 0, Occupancy: 4
```
