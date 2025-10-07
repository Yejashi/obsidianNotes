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


