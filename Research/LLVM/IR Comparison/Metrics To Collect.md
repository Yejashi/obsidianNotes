## A. Control-Flow & Structural Complexity

1. **Number of loops (total)**
    - Count natural loops via `LoopInfo`
    - Optionally stratify by **nesting depth**
2. **Maximum loop nesting depth**
    - Strong predictor of unrolling blow-ups
    - RAJA often introduces deeper nesting via lambdas
3. **Number of basic blocks**
    - Proxy for CFG complexity
    - Explains inlining and scheduling difficulty
4. **Number of branch instructions**
    - Conditional branches (`br i1`)
    - Correlates with divergence risk on GPUs
5. **Number of backedges**
    - Distinguishes “many small loops” vs “few large loops”
        

## B. Instruction Mix & IR Size
6. **Total instruction count**
    - Simple but very effective normalization metric
7. **Instruction count per basic block (avg / max)**
    - Large blocks → unrolling already happened
    - Very useful to confirm “pre-unrolled at -O1”
8. **Arithmetic instruction count**
    - `add`, `mul`, `fma`, etc.
    - Helps explain compute-bound vs memory-bound behavior
9. **Memory instruction count**
    - `load`, `store`, `atomic`
    - Particularly important for your spill analysis
10. **Call instruction count**
- Especially **indirect calls** (function pointers, lambdas)
    
- RAJA abstractions sometimes leave residue here
    

👉 **Why this matters:**  
When RAJA performs worse, you often see **higher instruction density + higher memory ops**, even when “doing the same math”.

---

## C. Loop Optimization Sensitivity (🔥 High Value for You)

_(“How likely is this function to be aggressively transformed?”)_

11. **Number of loop-invariant instructions**
    

- Count values that dominate all loop exits and are used inside loops
    
- Directly correlates with LICM opportunities
    

12. **Number of loops with constant trip counts**
    

- Via `ScalarEvolution`
    
- These loops are unroll magnets
    

13. **Estimated loop body size**
    

- Rolled body instruction count
    
- Useful to correlate with unroll-cost heuristics
    

14. **Number of PHI nodes**
    

- Especially loop-carried PHIs
    
- Strong proxy for register pressure
    

👉 **This is huge for your thesis story:**  
RAJA often exposes _more invariant expressions_, which:

> → increases LICM  
> → inflates live ranges  
> → increases register pressure  
> → triggers spills  
> → kills occupancy

These metrics let you _prove_ that pipeline.

---

## D. Register Pressure Proxies (No Backend Needed)

_(“How scary does this look to regalloc?”)_

You can’t see actual VGPR usage in IR—but you can get _very good proxies_.

15. **Maximum number of live SSA values per basic block**
    

- Simple liveness walk
    
- Strong predictor of VGPR pressure
    

16. **Average SSA use-count**
    

- Long-lived values = worse pressure
    

17. **Number of values with multiple uses across loop iterations**
    

- Flags values that survive unrolling badly
    

18. **Number of spills _predicted_ by backend remarks**
    

- Optional: correlate with `-pass-remarks-missed=regalloc`
    

👉 **This directly supports your MASS3DEA analysis**  
You can show:

> “RAJA produces more live values _before_ regalloc ever runs.”

---

## E. Memory Access Quality (GPU-Relevant)

_(“Are memory patterns becoming worse?”)_

19. **Number of GEP instructions**
    

- Proxy for address computation complexity
    

20. **Number of non-constant GEPs**
    

- Suggests poorer coalescing potential
    

21. **Loads/stores inside loops vs outside**
    

- Memory traffic amplification due to unrolling
    

22. **Pointer address space distribution**
    

- addrspace(1), addrspace(3), etc.
    
- Helpful for HIP / AMDGPU analysis
    

---

## F. Optional but Very Nice (If Time Allows)

23. **Inlining residue**
    

- Count functions that remain non-inlined but are called only once
    

24. **Lambda depth (RAJA-specific but IR-visible)**
    

- Infer via debug info or call chains
    
- Explains structural differences without hard-coding RAJA
    

25. **Vectorization eligibility**
    

- Count loops with no vectorization blockers (no calls, no atomics)