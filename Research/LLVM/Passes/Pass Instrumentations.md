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

Statistics and Profiling
- Developers can use pass instrumentations to gather statistics about passes, such as how many times a pass is run, its runtime, or its effects on the program.

Logging and Debugging
- They are often used to log detailed information about a pass, including which functions, loops, or regions it affects, and the transformations it applies.

### How it works
The core logic to run each Pass in the new PassManager is pretty easy to understand.
```cpp

```