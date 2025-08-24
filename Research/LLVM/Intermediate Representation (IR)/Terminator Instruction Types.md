- `ret` (ReturnInst):
    This instruction returns control from the current function. It can return a value or be a void return. It has no successors within the current function's control flow graph.
    
- `br` (BranchInst):
    This instruction performs a conditional or unconditional branch.
    - **Unconditional Branch:** `br label %dest_block` unconditionally transfers control to the specified basic block.
    - **Conditional Branch:** `br i1 %cond, label %true_block, label %false_block` transfers control to `%true_block` if `%cond` is true, and to `%false_block` otherwise.
    
- `switch` (SwitchInst):
    This instruction implements a multi-way branch based on an integer value. It takes an integer value, a default destination basic block, and a list of case-value/destination-block pairs. Control is transferred to the block corresponding to the matching case value, or to the default block if no match is found.
    
- `indirectbr` (IndirectBrInst):
    This instruction implements an indirect branch to a basic block specified by a pointer value. It takes a pointer to a basic block and a list of potential destination basic blocks.
    
- `invoke` (InvokeInst):
    This instruction represents a function call that might throw an exception. It specifies a normal destination basic block for successful execution and an unwind destination basic block for exceptional handling.
    
- `resume` (ResumeInst):
    This instruction is used to resume propagation of an exception after a `catch` block. It takes a `token` operand representing the exception.
    
- `unreachable` (UnreachableInst):
    This instruction indicates that control flow should never reach this point. It is used to mark code paths that are logically impossible or that represent error conditions where execution should not continue.