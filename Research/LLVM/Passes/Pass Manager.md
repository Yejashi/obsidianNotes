The LLVM Pass Manager is responsible for organizing and executing a sequence of transformations or analyses passes on the IR.

### Pass Manager Overview
LLVM provides several levels of Pass Managers depending on the scope of the pass:
- **FunctionPassManager**: Executes passes at the function level. Each function in the module is processed independently.
- **ModulePassManager**: Handles passes at the module level, which have access to the entire module.
- **LoopPassManager**: Focuses on loop transformations, operating within function-level passes.
- **CGSCCPassManager**: Operates on Call Graph Strongly Connected Components (SCCs), useful for inter-procedural analysis or optimizations.

### Legacy vs New Pass Manager
LLVM has two Pass Manager frameworks:
- **Legacy Pass Manager**: Older system with a simple API. It is still supported but being phased out.
- **New Pass Manager**: More efficient and flexible. Introduced to address the limitations of the legacy system, such as better support for parallelism and reduced overhead.

### Key Features of the Pass Manager
- **Dependency Management**: Ensures that prerequisite analysis passes are executed before transformation passes.
- **Invalidation**: Tracks whether the results of an analysis pass remain valid after a transformation pass modifies the IR.
- **Customization**: Users can create custom pipelines by combining LLVM’s predefined passes or their own.
### Workflow of the Pass Manager
- **Pass Registration:** Passes are registered with the pass manager.
- **Scheduling:** The pass manager determines the order of execution based on dependencies.
- **Execution:** The pass manager runs each pass in the scheduled order, ensuring that analysis results are available for dependent passes.




