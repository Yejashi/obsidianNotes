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

```
define i32 @example(i1 %cond) {
entry:                            ; First basic block (Node 1)
  %0 = add i32 1, 2               ; Instruction
  br i1 %cond, label %if.then, label %if.else ; Conditional branch

if.then:                          ; Second basic block (Node 2)
  %1 = mul i32 %0, 2              ; Instruction
  br label %if.end                ; Unconditional branch

if.else:                          ; Third basic block (Node 3)
  %2 = sub i32 %0, 1              ; Instruction
  br label %if.end                ; Unconditional branch

if.end:                           ; Fourth basic block (Node 4)
  %3 = phi i32 [ %1, %if.then ], [ %2, %if.else ] ; PHI node
  ret i32 %3                      ; Return statement
}
```

Corresponding CFG::
- Nodes: `entry`, `if.then`, `if.else`, `if.end`.
- Edges:
	- `entry` → `if.then` (True branch of `%cond`).
	- `entry` → `if.else` (False branch of `%cond`).
	- `if.then` → `if.end`.
	- `if.else` → `if.end`


### Importance of CFG
Control Flow Representation:
- Models all possible execution paths through a function.
- Forms the foundation for many compiler analyses and optimizations.

Data Flow Analysis:
- Tracks the flow of data (e.g., variable values) along paths in the CFG.
- Used in optimizations like constant propagation and dead code elimination.

Loop Analysis:
- Loops are easily identifiable as cycles in the CFG.
- LLVM uses CFGs for loop transformations (e.g., unrolling, vectorization).

