### What is LLVM?
LLVM (Low Level Virtual Machine) is in essence a compiler infrastructure filled with a collection of toolchains that can be used to :
- Build new computer languages
- Improve existing language
- Develop a frontend for any programming language
- Develop a backend for any instruction set architecture

### LLVM: Intermediate Representation (IR)
LLVM's Intermediate Representation is a platform-independent, low-level programming language. It serves as the "common ground" between source code and machine code.

**Characteristics:**
- LLVM's Intermediate Representation is a platform-independent, low-level programming language. It serves as the "common ground" between source code and machine code.
- Has a typed system and three representations: 
	- textual IR, 
	- binary bitcode, 
	- in-memory IR.

Example IR Code:
```llvm
define i32 @add(i32 %a, i32 %b) {
entry:
  %sum = add i32 %a, %b
  ret i32 %sum
}
```

### LLVM's Compilation Process
- Frontend
	- Converts source code (C, C++, Rust, etc.) to LLVM IR.
	- For example, Clang (C/C++) is a frontend for LLVM.
- Middle-end
	- Performs optimizations on the IR (e.g., removing redundant calculations, simplifying expressions).
	- Can include custom passes written by you.
- Backend
	- Converts the optimized IR into machine code for a specific architecture (e.g., x86, ARM).
	- Performs target-specific optimizations.

### Key Components
- LLVM Passes
	- LLVM passess are modular components that analyze or transform IR during the compilation process.
		- There are two type of passess:
		- Analysis Passes: Inspect IR and gather data (e.g., dependency graphs).
		- Transformation Passes: Modify IR (e.g., loop unrolling, inlining).
- LLVM Optimizer
	- A collection of passes used to improve the performance and efficiency of IR.
- LLVM Code Generator
	- LLVM Code Generator


