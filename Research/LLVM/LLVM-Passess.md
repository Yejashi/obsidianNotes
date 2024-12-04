LLVM passes are essential components of the LLVM compiler infrastructure, responsible for analyzing and transforming the Intermediate Representation (IR). Passes are modular, reusable units of work that can optimize, analyze, or transform LLVM IR during compilation. 

There are two primary types of passes in LLVM:
1. Analysis Passes: These examine the IR and gather information, but they don’t modify the code.
2. Transformation Passes: These modify the IR to optimize or transform the code, such as inlining functions, unrolling loops, or simplifying expressions.

### Overview of LLVM Passes
LLVM passes work in a sequence during the compilation process. They operate on the IR and can be organized into different stages of the pipeline:
- Frontend Passes: Perform parsing and initial translation from source code to LLVM IR.
- Optimization Passes (Middle-End): Perform transformations to improve the efficiency of the code, such as constant folding, loop unrolling, or dead code elimination.
- Target-Specific Passes (Backend): Focus on architecture-specific optimizations and target code generation.

Passes can be executed at different levels, including:
- Function Level: Operates on a single function.
- Module Level: Operates on the entire module, which could consist of multiple functions.

LLVM passes are designed to be composable, meaning you can create complex pass pipelines by chaining different passes together.
