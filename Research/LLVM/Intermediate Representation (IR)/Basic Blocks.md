A basic block is a straight-line sequence of instructions with no branching except at the end. 

A basic block has the following characteristics:
- Linear sequence: 
	- Contains instructions that execute sequentially
- Single Entry, Single Exit: 
	- Execution enters at the first instruction and exits at the last without branching in the middle.
- Control Flow: 
	- Ends with a terminator instruction (e.g., br for branching or ret for returning).

Basic blocks are the building blocks of LLVM IR's control flow graph (CFG), where:
- Nodes represent basic blocks
- Edges represent control flow transitions

### Structure
A basic block typically consists of:
- Label: Each block ash a unique label used for identification
- Instructions: A  series of LLVM IR instructions
- Terminator Instruction: A mandatory instruction at the end, which defines the control flow (e.g., branch to another block or function return).

Example:
```

```