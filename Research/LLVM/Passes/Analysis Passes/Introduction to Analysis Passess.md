In LLVM, analysis passes are a fundamental type of pass used to collect information about the program being compiled without making any modifications to the IR. 

These passes are crucial for optimization and transformation passes, which rely on the data collected by analysis passes to make decisions.

### Purpose of Analysis Passes
- **Gather Information**: Analysis passes analyze the intermediate representation (IR) of the code to collect insights such as control flow, dependencies, variable usage, and memory access patterns.
- **Provide Reusable Results**: The results of analysis passes can be cached and reused by multiple optimization passes to avoid redundant computations.
- **Support Other Passes**: They serve as the foundation for transformations and optimizations by providing accurate program metadata.

### Types of Analysis Passes
**Control Flow Analysis**: These passes analyze the structure and properties of the control flow graph (CFG) of functions.

**Data Flow Analysis**: These passes analyze how data moves through the program, enabling optimizations like dead code elimination and constant propagation.

**Profile-Guided Analysis**: These passes analyze profile-guided information (e.g., runtime behavior of programs).

**Loop-Specific Analysis**: Focused on analyzing and improving loops in the program.

**Inter-procedural Analysis**: These passes analyze multiple functions at a time to gather information about function interactions.


### Important things to consider
- **Preserved Analysis**: Some analysis passes are "preserved" when transformations occur, meaning their results remain valid. LLVM has mechanisms to specify which analyses are invalidated by a pass.
- **Lazy Evaluation**: Analysis passes are often lazily computed—only run when their results are requested by another pass.
