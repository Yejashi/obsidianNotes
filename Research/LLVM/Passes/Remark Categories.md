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


### What’s the difference between “missed” and “analysis”?
- **Missed (`OptimizationRemarkMissed`)**  
    Use this when the pass **intended to perform a specific transformation**, ran its **profitability/legality checks**, and **decided not to apply it** (or couldn’t). In other words: _“This optimization was considered for this IR, but it didn’t happen.”_  
    Examples:
    - **Inline**: “missed: no definition / too costly / recursive / cold callee.”  
        The inliner _evaluated the callsite_ and declined → **missed**.
    - **Loop Vectorize**: “missed: dependence prevents vectorization.”  
        The pass _ran the vectorization decision_ for that loop and declined → **missed**.
    - **Unroll**: “missed: trip count unknown; not profitable.”  
        It _tried to choose an unroll factor_, bailed → **missed**.
        
- **Analysis (`OptimizationRemarkAnalysis`)**  
    Use this for **informational or diagnostic context** that doesn’t assert “we attempted this optimization at this particular site and declined.” It’s for:
    - Explanations of why a thing **wouldn’t even be considered** (e.g., preconditions fail before a site-specific decision), or
    - **Verbose trace**/cost-model details to help the user understand what the pass saw, or
    - General **non-actionable** notes.  
        Examples:
	    - “loop is not in canonical form; skipping vectorizer pipeline stage” (broad context).
	    - Cost-model breakdowns (“estimated cost X, width Y”) that accompany a later **passed**/**missed**.
	    - Loop-fusion code using “candidate rejected because …” as an _analysis_ breadcrumb rather than declaring a **missed** at a specific fused pair.


|Situation|Emit|Rationale|
|---|---|---|
|We **applied** the transform at a specific site|**Passed**|“Success happened here.”|
|We **evaluated** the transform at a specific site and **didn’t apply**|**Missed**|“Opportunity existed; we declined/failed.”|
|We’re giving **context** (preconditions, cost breakdowns, broad notes), not declaring a site-specific decision|**Analysis**|“Info to understand decisions; not success/failure by itself.”|