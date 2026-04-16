| ID  | Metric                                     | Category | Structural / Semantic | What it catches                                     |             |
| --- | ------------------------------------------ | -------- | --------------------- | --------------------------------------------------- | ----------- |
| C1  | `numBranches`                              | Control  | Structural            | Total control flow volume                           |             |
| C2  | `numConditionalBranches`                   | Control  | Structural            | "Risky" branches (misprediction/divergence)         |             |
| C3  | `numLoops`                                 | Control  | Structural            | Loop count baseline                                 |             |
| C4  | `maxLoopDepth`                             | Control  | Structural            | Nesting complexity                                  |             |
| C5  | `numLoopsWithComputableTripCount`          | Control  | **Semantic**          | Compiler's knowledge of loop bounds                 |             |
| C6  | `numLoopsWithReloadedBound`                | Control  | **Semantic**          | Aliasing blocking loop bound hoisting               |             |
| C7  | `numLoopInvariantBranchesInLoops`          | Control  | **Semantic**          | Branches the compiler can/did identify as hoistable |             |
| C8  | `numSelectInsts`                           | Control  | **Semantic**          | Successful if-conversion (branch elimination)       |             |
| C9  | `numSwitchInsts`                           | Control  | Structural            | Multi-way dispatch (expensive on GPU)               |             |
| C10 | `numUnreachableBlocks`                     | Control  | **Semantic**          | Dead code elimination success                       |             |
| M1  | `numLoads`                                 | Memory   | Structural            | Memory read pressure                                |             |
| M2  | `numStores`                                | Memory   | Structural            | Memory write pressure                               |             |
| M3  | `numInnerLoopLoadStoreAddrSame`            | Memory   | **Semantic**          | Unpromoted read-modify-write (aliasing failure)     |             |
| M4  | `numPromotedLoadsInLoops`                  | Memory   | **Semantic**          | Successful load-to-register promotion               |             |
| M5  | `numLoopInvariantAddressLoadsInInnerLoops` | Memory   | **Semantic**          | Loads that should have been hoisted but weren't     |             |
| M6  | `numAllocaOriginInnerLoopAccesses`         | Memory   | **Semantic**          | Thread-local data access in hot loops               |             |
| M7  | `numArgOriginInnerLoopAccesses`            | Memory   | **Semantic**          | Opaque pointer access in hot loops                  |             |
| M8  | `numNoAliasArguments`                      | Memory   | **Semantic**          | Alias information available to compiler             |             |
| M9  | `numGEPsWithMultipleIndices`               | Memory   | Structural            | Multi-dimensional access complexity                 |             |
| M10 | `numMemcpyToAlloca`                        | Memory   | **Semantic**          | Data localization (closure copy pattern)            |             |
| P1  | `numFloatArithmeticInsts`                  | Compute  | Structural            | FP compute volume                                   |             |
| P2  | `numIntegerArithmeticInsts`                | Compute  | Structural            | Integer compute (often overhead)                    |             |
| P3  | `numMulFeedingAdd`                         | Compute  | **Semantic**          | FMA opportunity count                               |             |
| P4  | `numReductionPHIs`                         | Compute  | **Semantic**          | Successful reduction recognition                    |             |
| P5  | `numContractFlaggedFPOps`                  | Compute  | **Semantic**          | FP fusion eligibility                               |             |
| P6  | `numFastMathFPOps`                         | Compute  | **Semantic**          | Compiler's FP optimization freedom                  |             |
| P7  | `numInnerLoopFPOps`                        | Compute  | Structural            | Hot-path compute intensity                          |             |
| P8  | `numIntegerMulsInGEPChains`                | Compute  | **Semantic**          | Address computation overhead                        |             |
| P9  | `numCastInsts`                             | Compute  | Structural            | Type conversion overhead                            |             |
| P10 | `numCallsToMathFunctions`                  | Compute  | Structural + Semantic | Expensive math operation count                      |             |
| ID  | Metric                                     | Category | Type                  | Role                                                | Aggregation |
| C1  | `numBranches`                              | Control  | Structural            | Cost-Shape                                          | Sum         |
| C2  | `numConditionalBranches`                   | Control  | Structural            | Cost-Shape                                          | Sum         |
| C3  | `numLoops`                                 | Control  | Structural            | Cost-Shape                                          | Sum         |
| C4  | `maxLoopDepth`                             | Control  | Structural            | Cost-Shape                                          | Max         |
| C5  | `numLoopsWithComputableTripCount`          | Control  | Semantic              | Exposure                                            | Sum         |
| C6  | `numLoopsWithReloadedBound`                | Control  | Semantic              | Exposure                                            | Sum         |
| C7  | `numLoopInvariantCondBranchesInLoops`      | Control  | Semantic              | Exposure                                            | Sum         |
| C8  | `numSelectInsts`                           | Control  | Semantic              | Cost-Shape                                          | Sum         |
| C9  | `numSwitchInsts`                           | Control  | Structural            | Cost-Shape                                          | Sum         |
| C11 | `numPotentialLoopVersioningGuardPatterns`  | Control  | Semantic              | Exposure                                            | Sum         |
| C12 | `numDistinctLoopBodySignatures`            | Control  | Semantic              | Exposure                                            | Sum         |
| C13 | `numInnerLoopBasicBlocks`                  | Control  | Structural            | Cost-Shape                                          | Sum         |
| C14 | `numInnerLoopPHINodes`                     | Control  | Structural            | Cost-Shape                                          | Sum         |
| M1  | `numLoads`                                 | Memory   | Structural            | Cost-Shape                                          | Sum         |
| M2  | `numStores`                                | Memory   | Structural            | Cost-Shape                                          | Sum         |
| M3  | `numInnerLoopSharedLoadStorePtrs`          | Memory   | Semantic              | Exposure                                            | Sum         |
| M4a | `numLoadFedRecurrencePHIs`                 | Memory   | Semantic              | Exposure                                            | Sum         |
| M4b | `numStoreFedLoopCarriedPHIs`               | Memory   | Semantic              | Exposure                                            | Sum         |
| M5  | `numLoopInvariantAddressLoadsInInnerLoops` | Memory   | Semantic              | Exposure                                            | Sum         |
| M6  | `numAllocaOriginInnerLoopAccesses`         | Memory   | Semantic              | Exposure                                            | Sum         |
| M7  | `numArgOriginInnerLoopAccesses`            | Memory   | Semantic              | Exposure                                            | Sum         |
| M8  | `numNoAliasArguments`                      | Memory   | Semantic              | Exposure                                            | Sum         |
| M9  | `numGEPsWithMultipleIndices`               | Memory   | Structural            | Cost-Shape                                          | Sum         |
| M10 | `numMemcpyToAlloca`                        | Memory   | Semantic              | Exposure                                            | Sum         |
| M11 | `numInnerLoopDistinctBasePointers`         | Memory   | Semantic              | Cost-Shape                                          | Sum         |
| P1  | `numFloatArithmeticInsts`                  | Compute  | Structural            | Cost-Shape                                          | Sum         |
| P2  | `numIntegerArithmeticInsts`                | Compute  | Structural            | Cost-Shape                                          | Sum         |
| P3  | `numFMulSingleUseFAdd`                     | Compute  | Semantic              | Exposure                                            | Sum         |
| P4  | `numReductionPHIs`                         | Compute  | Semantic              | Exposure                                            | Sum         |
| P5  | `numContractFlaggedFPOps`                  | Compute  | Semantic              | Exposure                                            | Sum         |
| P6  | `numFastMathFPOps`                         | Compute  | Semantic              | Exposure                                            | Sum         |
| P7  | `numInnerLoopFPOps`                        | Compute  | Structural            | Cost-Shape                                          | Sum         |
| P8  | `numIntMulsInGEPChains`                    | Compute  | Semantic              | Cost-Shape                                          | Sum         |
| P9  | `numCastInsts`                             | Compute  | Structural            | Cost-Shape                                          | Sum         |
| P10 | `numCallsToMathFunctions`                  | Compute  | Structural + Semantic | Cost-Shape                                          | Sum         |
| P11 | `innerLoopFPToMemRatio`                    | Compute  | Semantic              | Density                                             | Max         |
| D1  | `innerLoopCFGDensity`                      | Derived  | Semantic              | Density                                             | Max         |
|     |                                            |          |                       |                                                     |             |
|     |                                            |          |                       |                                                     |             |


**Polybench_ADI**
The causal chain:
- ![[Screenshot_20260416_014817.png]]
**Yes, the metrics successfully capture and explain the 54% performance degradation.** The key signals are:

1. **C7 (invariant branches)** — identifies the root structural problem
2. **M4a (load-fed recurrence PHIs)** — identifies the missing optimization (store forwarding/load promotion)
3. **C11 (versioning guard patterns)** — identifies the missing loop versioning
4. **D1 (CFG density)** — quantifies the overhead impact
5. **C12 (distinct loop body signatures)** — contextualizes Native's higher instruction counts as versioning artifacts, not extra work

**Polybench_MVT**
**Yes, the metrics successfully capture and explain the 14% degradation.** The key discriminating metrics are:

- **C7** (invariant branch) — identifies the root structural problem
- **C13** (inner loop BBs) — quantifies the structural impact
- **C14** (inner loop PHIs) — quantifies the merge overhead
- **D1** (CFG density) — contextualizes the overhead relative to useful work
- **P11** (FP-to-mem ratio) — confirms the kernel is memory-bound, making overhead impactful

**Polybench_GESUMMV**
An analyst comparing GESUMMV to MVT would see:

1. **Both have the same RAJA overhead pattern**: C7 = 1, C13 = 3 (invariant branch splits loop into 3 BBs)
2. **GESUMMV has more useful work per iteration**: P7 = 4 vs 2, M11 = 3 vs 2, P4 = 2 vs 1
3. **D1 captures the difference**: GESUMMV RAJA D1 = 0.43 (below threshold) vs MVT RAJA D1 = 0.75 (above threshold)
4. **P11 confirms**: GESUMMV has higher arithmetic intensity (1.33 vs 1.0)

Conclusion: "GESUMMV has the same RAJA control flow overhead as MVT, but its inner loop does 2× the useful FP work (P7 = 4) on more data streams (M11 = 3), resulting in a D1 of 0.43 — low enough that the overhead is absorbed. MVT's D1 of 0.75 indicates the overhead dominates."

**Yes, the metrics correctly explain why GESUMMV performs similarly despite having the same overhead pattern as MVT.** The key metrics are:

- **D1** — directly discriminates: 0.43 (GESUMMV, overhead absorbed) vs 0.75 (MVT, overhead dominates)
- **P7** — explains why: 4 FP ops/iter (GESUMMV) vs 2 (MVT) — more work to amortize against
- **M11** — reinforces: 3 arrays (GESUMMV) vs 2 (MVT) — more memory traffic per iteration
- **C7, C13** — confirm the overhead pattern is identical between the two kernels