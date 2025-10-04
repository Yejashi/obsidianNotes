**LLVM IR** – a target-independent intermediate representation (IR) for compiler optimization and code generation.

Compared to Clang's **Abstract Syntax Tree (AST)**, LLVM IR provides a different level of abstraction by encapsulating extra execution details to enable more powerful program analyses and transformations.

### Writing an LLVM Pass with the new PassManager
A Pass in LLVM is the basic unit that is required to perform certain actions against LLVM IR.

LLVM also consists of multiple Passes that are executed in sequential order, called the Pass pipeline. Figure 9.1 shows an example of the Pass pipeline:

![[Pasted image 20251004172141.png]]

In the preceding diagram, multiple Passes are arranged in a straight line. The LLVM IR for the foo function is processed by one Pass after another.

Pass B, for instance, performs code optimization on foo and replaces an arithmetic multiplication (mul) by 2 with left shifting (shl) by 1, which is considered easier than multiplication in most hardware architectures.

In addition, this figure also illustrates that the **code generation** steps are modeled as Passes. Code generation in LLVM transforms LLVM IR, which is target independent, into assembly code for certain hardware architecture (for example, x86_64 in Figure 9.1). 


#### Code Generation Passes
