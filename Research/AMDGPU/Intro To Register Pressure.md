**Sources**:
- Video: https://vimeo.com/742349001
- PDF: https://www.olcf.ornl.gov/wp-content/uploads/Intro_Register_pressure_ORNL_20220812_2083.pdf

### Register Pressure and Performance
The performance of GPU kernels is highly dependent on "occupancy", where there are various wavefronts (warps) running in parallel.
- **Occupancy** is the fraction of the GPU’s maximum hardware execution capacity that is actively utilized by  wavefronts (warps) on a compute unit.
- Basically, the ratio of active wavefronts per SM/CU to the maximum wavefronts the hardware can support simultaneously.

GPUs execute many wavefronts (warps) in parallel on each compute unit and occupancy determines how many of these wavefronts can be resident and ready to run at the same time.

Occupancy is determined by the per-wavefront consumption of hardware resources, such as registers and shared memory (LDS).

Because these resources are allocated on a per-kernel basis, a kernel that uses more registers or LDS per wavefront reduces the number of wavefronts that can be simultaneously resident on a compute unit.

As a result, high per-wave resource usage lowers occupancy by limiting the number of concurrent waves per CU.

Basically, each compute unit has a fixed budget of registers and shared memory. When a kernel launches, each wavefront reserves a portion of these resources. If a kernel requires many registers, fewer wavefronts can fit within the CU’s resource limits, meaning fewer waves can run in parallel. This reduces occupancy and can limit the GPU’s ability to hide memory and instruction latency.

The number of registers used by a wavefront is determined by the compiler’s register allocation phase.

##### Intuition
Each compute unit (CU) has a fixed pool of hardware resources, such as:
- Registers (VGPRs / SGPRs)
- Shared memory (LDS)
- Execution slots for waves

When a kernel is launched:
- Every wave of that kernel gets its own private slice of these resources
- The hardware must reserve those resources **before the wave can become resident**

Key idea
> **Occupancy = how many waves can fit on a CU at the same time, given resource limits.**

Simple kernel vs Complex Kernel

**Case A: Simple Kernel (few registers, little LDS)**
Example:
```
C[i] = A[i] + B[i];
```
- Few instructions
- Few live variables
- Low register usage per thread
- Little or no shared memory

What happens:
- Each wave uses very few registers
- The CU can fit many waves simultaneously
- Result: high occupancy

Each wave is “cheap”, so you can pack lots of them onto the CU

**Case B: Complex kernel (many registers, many operations)**
Example:
- Deeply nested loops
- Large unrolled loops
- Many temporary values
- Heavy math or address computation

High register pressure, Many live values at once.

What happens:
- Each wave requires many registers
- The CU runs out of registers quickly
- Only a few waves can be resident
- Result: low occupancy

Each wave is “expensive”, so only a few can fit on the CU at once.


Register spilling happens when register pressure exceeds the available physical registers, forcing the compiler to temporarily store some values in memory (scratch / local memory) instead of keeping them in registers.


### Compromises for Register Allocation
Register allocation is NP-Hard problem.

Compilers compromise on correctness by applying “heuristics” that produce mostly correct solutions.

Compilers not only optimize for occupancy but also for instruction-level parallelism (ILP, minimizing the schedule length).

The two are in conflict: higher ILP requires more registers, which decreases occupancy.

In codes with high register pressure, obtaining a good ILP can make a difference on the final performance.

Occupancy is more important than ILP.


### Scratch Use

What is scratch, and why does my program use it?
- Scratch is per-thread memory in global memory used as a fallback when values cannot be kept in registers (or LDS).
- So HBM but thread local.
- It is entirely managed by the compiler and GPU runtime.

Where does scratch use come from?
- The popular notion that scratch use only comes from register spilling is not always true. It comes from two possible options:
	- Register spilling: f enough registers are not available, variables will be "spilled" to scratch memory. The compiler keeps track of variable liveness and tries to maximize reuse and minimize spilling (NP-Hard problem)
		- Spilling is not always bad. Enough occupancy can hide the extra, more costly, memory access
			- The goal is occupancy. If the compiler can spill a little but get you higher overall occupancy then your performance goes up.
	- Memory objects : Any variable is naturally a memory object. The compiler may attempt to place it to registers or LDS, but this may not succeed (e.g., due to size of an object


### How to Identify Scratch Use and Spilling

Looking at the ISA (assembly) is the simplest way.

`--save-temps` generated ISA files with valuable statistics on register and scratch usage and pills.
- Caveat: In some cases --save-temps can change the generated ISA

Direct indicators of spills (in --save-temps):
- Look for`.sgpr_spill_count` and `.vgpr_spill_count` fields
- When compiling with debug symbols, look for comments like `4-Byte Folded Spill`

Direct indicators of scratch use (in --save-temps):
- Look for non zero `ScratchSize XX` in metadata after a given kernel

Indirect indicators of scratch use (also available in disassembly):
- Look for instructions like `buffer_store_dword v18, off, s[0:3], 0 offset:160`

Using remarks for spills:
- `-Rpass-analysis=kernel-resource-usage`


### How to Reduce Register Spilling

Avoid allocating on the stack in a kernel
- Memory allocated on the stack lives in scratch and may be optimized into registers

Avoid passing big object as argument in kernels
- Function arguments are allocated on the stack and may be optimized into registers


Avoid writing large kernels with many function calls
- All device functions are inlined. A kernel calling many device functions can become very big

Keep loop unrolling under control
- 
