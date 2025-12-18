#### Middle-End
1. Number of Loops
2. Max loop depth
3. Number of Basic blocks
4. Number of Branches
5. Number of Function calls
6. Total instruction count
7. Arithmetic instruction count
8. Memory instruction count
9. Number of PHI nodes
10. Number of Loop-invariant instructions
11. Number of Constant-trip loops
12. Avg instructions per BB
13. Max live SSA values
14. Number of GEP instructions
15. Loads/stores inside loops


What that will look like:
```
{
  "module": "MASS3DEA-Hip.cpp.o",
  "opt_level": "O2",
  "functions": [
    {
      "name": "_ZN8rajaperf4apps8Mass3DEAILm64EEEvPdS2_S2_",
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

#### Backend

Backend:
```
hipcc your_kernel.cpp -O3 -Rpass-analysis=kernel-resource-usage
```

```
remark: kernel-resource-usage: KernelName VGPRs: 64, SGPRs: 24, ScratchSize: 0, VGPRSpills: 0, SGPRSpills: 0, Occupancy: 4
```

Can this be done programmatically through a library?

| Tool                   | Backing library               |
| ---------------------- | ----------------------------- |
| `llvm-readobj`         | `llvm::object`                |
| `llvm-objdump`         | `llvm::object` + `llvm::MC`   |
| AMDGPU kernel metadata | `llvm::AMDGPU`                |
| Code object parsing    | `llvm::object::ELFObjectFile` |

What would this look like?
A **standalone analysis tool** (linked against LLVM) that:
1. Loads the `.o` / `.hsaco` / binary
2. Parses AMDGPU kernel metadata
3. Optionally disassembles kernels
4. Emits structured JSON

