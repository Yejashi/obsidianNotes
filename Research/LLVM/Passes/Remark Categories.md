The **three remark classes** LLVM uses:
- **Passed** → `OptimizationRemark`  
    “The optimization **was applied**.”
- **Missed** → `OptimizationRemarkMissed`  
    “We **wanted to apply** this optimization but **couldn’t** (legality/profitability).”
- **Analysis** → `OptimizationRemarkAnalysis`  
    “Here’s **information/diagnosis**; not asserting success or failure.”

Clang flags map to those classes:
- `-Rpass=...` → shows **Passed**
- `-Rpass-missed=...` → shows **Missed**
- `-Rpass-analysis=...` → shows **Analysis**


