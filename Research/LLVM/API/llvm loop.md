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

