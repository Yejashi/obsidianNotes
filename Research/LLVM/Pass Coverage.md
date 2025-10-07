|Category|Pass Name|Remark Types|
|---|---|---|
|Inlining|`inline`, `always-inline`, `partial-inliner`, `module-inline`|“inlined call”, “missed inlining”, “inline cost”|
|Vectorization|`loop-vectorize`, `slp-vectorizer`, `loop-idiom-vectorize`|“vectorized loop”, “failed vectorization”|
|Loop unrolling|`loop-unroll`, `loop-unroll-and-jam`, `loop-unroll-full`|“fully unrolled”, “unroll-not-profitable”|
|LICM|`licm`, `lnicm`, `loop-versioning-licm`|“hoisted load”, “not-hoisted”|
|InstCombine|`instcombine`, `aggressive-instcombine`|“folded instruction”|
|SimplifyCFG|`simplifycfg`|“simplified branch”|
|Loop distribution|`loop-distribute`|“distributed loop”|
|Loop predication|`loop-predication`|“predicated branch”|
|DSE / MemCpyOpt|`dse`, `memcpyopt`|“removed store”, “merged memcpy”|
|Speculative execution|`speculative-execution`|“speculated instruction”|
|GVN / NewGVN|`gvn`|“redundant load eliminated”|
|Attributor|`attributor`, `attributor-light`|“deduced attribute”|
|PGO passes|`pgo-icall-prom`, `pgo-memop-opt`|“promoted indirect call”, “memop size optimized”|


| Category                   | Pass                                                                                                                                                                                          | Significance                                         | Notes                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Loop transformations**   | `loop-fusion`, `loop-interchange`, `loop-flatten`, `loop-reduce` (LoopStrengthReduce), `loop-sink`, `loop-deletion`, `loop-simplify`, `loop-term-fold`, `loop-bound-split`, `loop-versioning` | Huge runtime impact (memory locality, structure)     | 🟥 **No remarks** — still completely silent (even the new `loop-fusion` implementation) |
| **Scalar / memory**        | `sroa`, `mem2reg`, `scalarizer`, `sink`, `reg2mem`, `flatten-cfg`, `nary-reassociate`, `reassociate`, `float2int`, `slpsr`, `slsr`                                                            | Canonicalization and strength-reduce that reshape IR | 🟥 **Silent** — these are foundational and often change alias patterns but emit nothing |
| **Interprocedural**        | `argpromotion`, `globalopt`, `globaldce`, `function-import`, `internalize`, `wholeprogramdevirt`, `mergefunc`                                                                                 | Affect call graph and linkage                        | 🟥 **Silent**, no diagnostic despite major semantic changes                             |
| **CFG / structural**       | `lower-invoke`, `lower-switch`, `lower-expect`, `structurizecfg`, `unify-loop-exits`, `break-crit-edges`                                                                                      | Modify control flow drastically                      | 🟥 **Silent**                                                                           |
| **Prefetch / HW specific** | `loop-data-prefetch`, `hardware-loops`, `interleaved-access`, `interleaved-load-combine`                                                                                                      | Performance-critical on CPUs/GPUs                    | 🟥 **Silent**                                                                           |
| **Miscellaneous**          | `guard-widening`, `loop-idiom`, `loop-idiom-vectorize`, `make-guards-explicit`, `infer-alignment`                                                                                             | Minor but measurable effect                          | `loop-idiom` may emit some, others silent                                               |