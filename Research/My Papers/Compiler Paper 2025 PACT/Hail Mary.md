<<<<<<< HEAD
| ID  | Metric                                     | Category | Structural / Semantic | What it catches                                     |
| --- | ------------------------------------------ | -------- | --------------------- | --------------------------------------------------- |
| C1  | `numBranches`                              | Control  | Structural            | Total control flow volume                           |
| C2  | `numConditionalBranches`                   | Control  | Structural            | "Risky" branches (misprediction/divergence)         |
| C3  | `numLoops`                                 | Control  | Structural            | Loop count baseline                                 |
| C4  | `maxLoopDepth`                             | Control  | Structural            | Nesting complexity                                  |
| C5  | `numLoopsWithComputableTripCount`          | Control  | **Semantic**          | Compiler's knowledge of loop bounds                 |
| C6  | `numLoopsWithReloadedBound`                | Control  | **Semantic**          | Aliasing blocking loop bound hoisting               |
| C7  | `numLoopInvariantBranchesInLoops`          | Control  | **Semantic**          | Branches the compiler can/did identify as hoistable |
| C8  | `numSelectInsts`                           | Control  | **Semantic**          | Successful if-conversion (branch elimination)       |
| C9  | `numSwitchInsts`                           | Control  | Structural            | Multi-way dispatch (expensive on GPU)               |
| C10 | `numUnreachableBlocks`                     | Control  | **Semantic**          | Dead code elimination success                       |
| M1  | `numLoads`                                 | Memory   | Structural            | Memory read pressure                                |
| M2  | `numStores`                                | Memory   | Structural            | Memory write pressure                               |
| M3  | `numInnerLoopLoadStoreAddrSame`            | Memory   | **Semantic**          | Unpromoted read-modify-write (aliasing failure)     |
| M4  | `numPromotedLoadsInLoops`                  | Memory   | **Semantic**          | Successful load-to-register promotion               |
| M5  | `numLoopInvariantAddressLoadsInInnerLoops` | Memory   | **Semantic**          | Loads that should have been hoisted but weren't     |
| M6  | `numAllocaOriginInnerLoopAccesses`         | Memory   | **Semantic**          | Thread-local data access in hot loops               |
| M7  | `numArgOriginInnerLoopAccesses`            | Memory   | **Semantic**          | Opaque pointer access in hot loops                  |
| M8  | `numNoAliasArguments`                      | Memory   | **Semantic**          | Alias information available to compiler             |
| M9  | `numGEPsWithMultipleIndices`               | Memory   | Structural            | Multi-dimensional access complexity                 |
| M10 | `numMemcpyToAlloca`                        | Memory   | **Semantic**          | Data localization (closure copy pattern)            |
| P1  | `numFloatArithmeticInsts`                  | Compute  | Structural            | FP compute volume                                   |
| P2  | `numIntegerArithmeticInsts`                | Compute  | Structural            | Integer compute (often overhead)                    |
| P3  | `numMulFeedingAdd`                         | Compute  | **Semantic**          | FMA opportunity count                               |
| P4  | `numReductionPHIs`                         | Compute  | **Semantic**          | Successful reduction recognition                    |
| P5  | `numContractFlaggedFPOps`                  | Compute  | **Semantic**          | FP fusion eligibility                               |
| P6  | `numFastMathFPOps`                         | Compute  | **Semantic**          | Compiler's FP optimization freedom                  |
| P7  | `numInnerLoopFPOps`                        | Compute  | Structural            | Hot-path compute intensity                          |
| P8  | `numIntegerMulsInGEPChains`                | Compute  | **Semantic**          | Address computation overhead                        |
| P9  | `numCastInsts`                             | Compute  | Structural            | Type conversion overhead                            |
| P10 | `numCallsToMathFunctions`                  | Compute  | Structural + Semantic | Expensive math operation count                      |

| ID  | Metric                                         | Category | Type                  | Aggregation |
| --- | ---------------------------------------------- | -------- | --------------------- | ----------- |
| C1  | `numBranches`                                  | Control  | Structural            | Sum         |
| C2  | `numConditionalBranches`                       | Control  | Structural            | Sum         |
| C3  | `numLoops`                                     | Control  | Structural            | Sum         |
| C4  | `maxLoopDepth`                                 | Control  | Structural            | Max         |
| C5  | `numLoopsWithComputableTripCount`              | Control  | Semantic              | Sum         |
| C6  | `numLoopsWithReloadedBound`                    | Control  | Semantic              | Sum         |
| C7  | `numLoopInvariantBranchesInLoops`              | Control  | Semantic              | Sum         |
| C8  | `numSelectInsts`                               | Control  | Semantic              | Sum         |
| C9  | `numSwitchInsts`                               | Control  | Structural            | Sum         |
| C10 | `numUnreachableBlocks`                         | Control  | Semantic              | Sum         |
| C11 | `numLoopVersioningChecks`                      | Control  | Semantic              | Sum         |
| C12 | `numUniqueLoopBodies`                          | Control  | Semantic              | Sum         |
| C13 | `numInnerLoopBasicBlocks`                      | Control  | Structural            | Sum         |
| C14 | `numInnerLoopPHINodes`                         | Control  | Structural            | Sum         |
| M1  | `numLoads`                                     | Memory   | Structural            | Sum         |
| M2  | `numStores`                                    | Memory   | Structural            | Sum         |
| M3  | `numInnerLoopLoadStoreAddrSame`                | Memory   | Semantic              | Sum         |
| M4a | `numLICMPromotedLoads`                         | Memory   | Semantic              | Sum         |
| M4b | `numStoreForwardedLoads`                       | Memory   | Semantic              | Sum         |
| M5  | `numLoopInvariantAddressLoadsInInnerLoops`     | Memory   | Semantic              | Sum         |
| M6  | `numAllocaOriginInnerLoopAccesses`             | Memory   | Semantic              | Sum         |
| M7  | `numArgOriginInnerLoopAccesses`                | Memory   | Semantic              | Sum         |
| M8  | `numNoAliasArguments`                          | Memory   | Semantic              | Sum         |
| M9  | `numGEPsWithMultipleIndices`                   | Memory   | Structural            | Sum         |
| M10 | `numMemcpyToAlloca`                            | Memory   | Semantic              | Sum         |
| M11 | `numInnerLoopDistinctArrayAccesses`            | Memory   | Semantic              | Sum         |
| P1  | `numFloatArithmeticInsts`                      | Compute  | Structural            | Sum         |
| P2  | `numIntegerArithmeticInsts`                    | Compute  | Structural            | Sum         |
| P3  | `numMulFeedingAdd`                             | Compute  | Semantic              | Sum         |
| P4  | `numReductionPHIs`                             | Compute  | Semantic              | Sum         |
| P5  | `numContractFlaggedFPOps`                      | Compute  | Semantic              | Sum         |
| P6  | `numFastMathFPOps`                             | Compute  | Semantic              | Sum         |
| P7  | `numInnerLoopFPOps`                            | Compute  | Structural            | Sum         |
| P8  | `numIntegerMulsInGEPChains`                    | Compute  | Semantic              | Sum         |
| P9  | `numCastInsts`                                 | Compute  | Structural            | Sum         |
| P10 | `numCallsToMathFunctions`                      | Compute  | Structural + Semantic | Sum         |
| P11 | `innerLoopArithmeticIntensity`                 | Compute  | Semantic              | Max         |
| D1  | `innerLoopControlIntensity` (C13 / (P7 = M11)) | Derived  | Semantic              | max         |
=======
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
>>>>>>> origin/main


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


**Apps_FIR**
This is a striking case. Almost every inner-loop metric is **identical** between Native and RAJA:

- Same loops (C3=3), same depth (C4=2), same inner loop BBs (C13=2), same PHIs (C14=6)
- Same FP work (P1=10, P7=10), same reductions (P4=2), same FMA opportunities (P3=5)
- Same arithmetic intensity (P11=1.0), same CFG density (D1=0.25)
- Same loop signatures (C12=3), same invariant branches (C7=3)
- No blocked optimizations in either (M4a=0, M4b=0, C11=0 for both)



# Vizualization
Three heatmaps is the right call, but I'd suggest a specific layout:

**Rows** = kernels (one per row) **Columns** = metrics within that category **Color** = signed normalized difference (diverging colormap: blue = Native better, red = RAJA better, white = same) **Cell text** = `N→R` (e.g., `0→5`) for the raw values

This lets you scan vertically to see which metrics consistently differ across kernels, and horizontally to see the full metric profile for a single kernel.

**For the paper, the reading pattern is:**

1. **Scan columns** to find metrics that consistently differ across kernels (e.g., C7 is red for all RAJA-slower kernels)
2. **Scan rows** to see the full profile of a single kernel (e.g., FIR's row is mostly white except M6/M7/M10)
3. **Compare rows** to understand why similar kernels behave differently (e.g., MVT vs GESUMMV — same C7/C13 pattern but different D1)

**For your heuristics**, the heatmaps naturally suggest rules like:

- "If C7 > 0 and D1 > 0.5, expect RAJA slowdown" (MVT pattern)
- "If M6 > 0 and M7 = 0 and M10 > 0, expect RAJA speedup from data locality" (FIR pattern)
- "If M4a drops to 0 and C11 drops to 0, expect significant RAJA slowdown from blocked optimizations" (ADI pattern)



# **FINAL IR METRICS**

| Category | Metric                                     | Description                                                                                                                                        |
| -------- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Control  | `numLoops`                                 | Total number of natural loops detected by LLVM's LoopInfo                                                                                          |
| Control  | `maxLoopDepth`                             | Maximum loop nesting depth across all loops                                                                                                        |
| Control  | `numLoopsWithComputableTripCount`          | Number of loops where ScalarEvolution can determine the backedge-taken count                                                                       |
| Control  | `numLoopInvariantBranchesInsideLoop`       | Number of conditional branches inside loops whose condition does not change across iterations                                                      |
| Control  | `numSelectInsts`                           | Number of branchless conditional select instructions (if-conversion results)                                                                       |
| Control  | `numPotentialLoopVersioningGuardPatterns`  | Number of runtime alias-check patterns that guard versioned loop copies (heuristic detection)                                                      |
| Control  | `numDistinctLoopBodySignatures`            | Number of loops with structurally unique bodies based on instruction-count signatures                                                              |
| Control  | `numInnerLoopBasicBlocks`                  | Total number of basic blocks across all innermost loops                                                                                            |
| Control  | `numInnerLoopPHIInsts`                     | Total number of PHI nodes across all innermost loops                                                                                               |
| Control  | `innerLoopControlIntensity`                | Max ratio of inner loop basic blocks to useful operations (FP ops + distinct base pointers) across all inner loops                                 |
| Memory   | `numLoadInsts`                             | Total number of load instructions                                                                                                                  |
| Memory   | `numStoreInsts`                            | Total number of store instructions                                                                                                                 |
| Memory   | `numInnerLoopLoadStoreAddrSame`            | Number of distinct SSA pointers that appear as both a load and store operand in the same inner loop                                                |
| Memory   | `numLICMPromotedLoads`                     | Number of loop-header PHI nodes fed by a preheader load whose latch value recurs through the PHI, with a matching-address store in the loop        |
| Memory   | `numStoreForwardedLoads`                   | Number of loop-header PHI nodes fed by a preheader load whose latch value is also the operand of a store to the same underlying object in the loop |
| Memory   | `numLoopInvariantAddressLoadsInInnerLoops` | Number of load instructions in innermost loops whose pointer operand is loop-invariant                                                             |
| Memory   | `numAllocaOriginInnerLoopAccesses`         | Number of load/store instructions in innermost loops whose base pointer traces back to a stack allocation (alloca)                                 |
| Memory   | `numArgOriginInnerLoopAccesses`            | Number of load/store instructions in innermost loops whose base pointer traces back to a function argument                                         |
| Memory   | `numMemcpyToAlloca`                        | Number of llvm.memcpy intrinsic calls whose destination traces back to a stack allocation                                                          |
| Memory   | `numInnerLoopDistinctBasePointers`         | Number of distinct underlying memory objects accessed by loads and stores in innermost loops                                                       |
| Compute  | `numFloatArithmeticInsts`                  | Total number of floating-point arithmetic instructions (fadd, fsub, fmul, fdiv, frem, fneg)                                                        |
| Compute  | `numIntegerArithmeticInsts`                | Total number of integer arithmetic instructions (add, sub, mul, sdiv, udiv, srem, urem)                                                            |
| Compute  | `numMulFeedingAdd`                         | Number of fmul instructions whose single use is an fadd instruction (FMA opportunity proxy)                                                        |
| Compute  | `numReductionLikePHIs`                     | Number of loop-header PHI nodes that implement a reduction pattern through an associative arithmetic recurrence                                    |
| Compute  | `numContractFlaggedFPOps`                  | Number of floating-point instructions with the contract fast-math flag set (eligible for FMA fusion)                                               |
| Compute  | `numInnerLoopFloatArithmeticInsts`         | Total number of floating-point arithmetic instructions across all innermost loops                                                                  |
| Compute  | `numMulFeedingGEP`                         | Number of integer multiply or shift instructions whose result feeds into a getelementptr within a bounded use chain                                |
| Compute  | `numCastInsts`                             | Total number of type conversion instructions (sext, zext, trunc, fpext, fptrunc, sitofp, etc.)                                                     |
| Compute  | `innerLoopFPToMemRatio`                    | Max ratio of floating-point arithmetic instructions to memory instructions (loads + stores) across all innermost loops                             |
