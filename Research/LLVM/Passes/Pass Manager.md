The LLVM Pass Manager is responsible for organizing and executing a sequence of transformations or analyses passes on the IR.

### Pass Manager Overview
LLVM provides several levels of Pass Managers depending on the scope of the pass:
- **FunctionPassManager**: Executes passes at the function level. Each function in the module is processed independently.
- **ModulePassManager**: Handles passes at the module level, which have access to the entire module.
- **LoopPassManager**: Focuses on loop transformations, operating within function-level passes.
- **CGSCCPassManager**: Operates on Call Graph Strongly Connected Components (SCCs), useful for inter-procedural analysis or optimizations.


