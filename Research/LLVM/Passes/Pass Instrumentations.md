In LLVM, **pass instrumentations** are mechanisms that allow developers to hook into the execution of passes for various purposes such as analysis, debugging, profiling, or diagnostics.

### Key Features of Pass Instrumentations
Hooks for Pre/Post Execution
- Instrumentations provide hooks that are called before and after the execution of a pass
- For example:
	- `BeforePassExecution`: Called just before a pass is executed
	- `AfterPassExecution`: Called immediately after a pass finishes execution

Error Handling
- Pass instrumentations allow you to catch exceptions or errors raised during the execution of a pass, ensuring robust diagnostics and logging.

Analysis Preservation
- Instrumentations can track which analyses are invalidated or preserved after a pass is run, aiding in optimizing the order of passes and reducing redundant computations.