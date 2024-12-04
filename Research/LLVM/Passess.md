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

### Types of LLVM Passes
##### Analysis Passes
These passes gather information about the code but do not modify it.

Some Examples include:
- Data Structure Analysis: Analyzes loops, control flow, and data dependencies. For example, `LoopInfo` analyzes the loops in a function.
- Control Flow Analysis: Identifies how different blocks in a function are connected (e.g., through branches and loops). This is done by passes like `CFG` (Control Flow Graph).
- Alias Analysis: Analyzes pointers to determine whether two pointers might reference the same memory location.

##### Transformation Passes
These passes modify the IR to optimize it or transform it for better performance.

Common transformation passes include:
- Dead Code Elimination (DCE): Removes unused or redundant code.
- Constant Propagation: Replaces variables that have constant values with those constant values.
- Loop Unrolling: Expands loops to remove the overhead of the loop control code.
- Function Inlining: Replaces a function call with the body of the function, eliminating the call overhead.

##### Custom Passes
You can write your own custom passes to achieve specific goals, such as optimizing specific patterns or gathering statistics on optimization attempts, like the number of transformations applied per function.

There are three main ways to create custom passes in LLVM:
1. Function Passes: Operate on individual functions. These are useful for optimizations that only make sense on a function level, like inlining or loop unrolling.
2. Module Passes: Operate on the whole module (e.g., optimizations across functions).
3. Analysis Passes: These are typically used to gather data about the IR (e.g., tracking the number of times a particular transformation occurs).


### Pass Manager
LLVM passes are managed through a Pass Manager.

It organizes and runs passes in the correct order. Passes in LLVM are usually run in a pipeline, where each pass takes the output of the previous one and modifies it further.