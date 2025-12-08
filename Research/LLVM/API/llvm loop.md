### What `llvm::Loop` _is_
`llvm::Loop` is an abstract representation of a loop detected by **LoopInfo** (the analysis pass). It stores:
- The loop header block
- All basic blocks inside the loop
- The preheader
- The latch block(s)
- The exiting/exited blocks
- Loop nesting (subloops)
- Canonicalization info (is it simplified? LCSSA?)
- Induction variables (via LoopInfo + ScalarEvolution)
- Metadata (vectorization hints, unroll hints, etc.)

It does _not_ contain instructions—it references the corresponding `BasicBlock`s.

### **When `llvm::Loop` is used**
LLVM uses `llvm::Loop` at multiple phases in the middle-end:

##### **1. During analysis passes**
`llvm::Loop` is used for understanding a function’s control-flow shape:
- **LoopInfo** builds all `llvm::Loop` objects from the function’s CFG.
- **ScalarEvolution (SE)** uses loops to build induction-variable recurrences.
- **DominatorTree** + LoopInfo determine loop nesting structure.

##### **2. During optimization passes (most common use-case)**
A ton of optimization passes rely on `llvm::Loop`:

###### **Loop Canonicalization**

- `-loop-simplify` uses `llvm::Loop` to ensure:
    - one preheader
    - one latch
    - well-defined exit blocks
###### **LCSSA transformation**
- `LCSSA` uses `llvm::Loop` to insert PHIs on loop exits.
###### **Loop Unrolling**
Inside `LoopUnrollPass`:
```
for (Loop *L : LI) {
    // decide if L is unrollable
    UnrollLoop(L, ...);
}
```

##### **3. Loop Metadata / Hints**
`llvm::Loop` is also used when LLVM interprets loop metadata:
- `llvm.loop.unroll.disable`
- `llvm.loop.vectorize.enable`
- `llvm.loop.interleave.count`
- profiling hints
    
Passes query or modify metadata via:
```
MDNode *LoopMD = L->getLoopID();
```


### **How `llvm::Loop` is created**
