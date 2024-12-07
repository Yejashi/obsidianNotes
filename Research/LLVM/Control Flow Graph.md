The Control Flow Graph (CFG) in LLVM represents the flow of control between basic blocks in a function. 

It is a directed graph where:
- Nodes represent basic blocks
- Edges represent possible transfers of control between blocks

### Structure
- Nodes (Basic Blocks): Each basic block is a single node in the CFG. 
- Edges (Control Flow): Directed edges connect nodes based on the control flow. For example:
	- A conditional branch (`br i1`) creates two edges, one for each target block.
	- An unconditional branch (`br label`) creates a single edge.
	- Function return (`ret`) has no outgoing edges.

