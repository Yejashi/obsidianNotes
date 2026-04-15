|ID|Metric|Category|Structural / Semantic|What it catches|
|---|---|---|---|---|
|C1|`numBranches`|Control|Structural|Total control flow volume|
|C2|`numConditionalBranches`|Control|Structural|"Risky" branches (misprediction/divergence)|
|C3|`numLoops`|Control|Structural|Loop count baseline|
|C4|`maxLoopDepth`|Control|Structural|Nesting complexity|
|C5|`numLoopsWithComputableTripCount`|Control|**Semantic**|Compiler's knowledge of loop bounds|
|C6|`numLoopsWithReloadedBound`|Control|**Semantic**|Aliasing blocking loop bound hoisting|
|C7|`numLoopInvariantBranchesInLoops`|Control|**Semantic**|Branches the compiler can/did identify as hoistable|
|C8|`numSelectInsts`|Control|**Semantic**|Successful if-conversion (branch elimination)|
|C9|`numSwitchInsts`|Control|Structural|Multi-way dispatch (expensive on GPU)|
|C10|`numUnreachableBlocks`|Control|**Semantic**|Dead code elimination success|
|M1|`numLoads`|Memory|Structural|Memory read pressure|
|M2|`numStores`|Memory|Structural|Memory write pressure|
|M3|`numInnerLoopLoadStoreAddrSame`|Memory|**Semantic**|Unpromoted read-modify-write (aliasing failure)|
|M4|`numPromotedLoadsInLoops`|Memory|**Semantic**|Successful load-to-register promotion|
|M5|`numLoopInvariantAddressLoadsInInnerLoops`|Memory|**Semantic**|Loads that should have been hoisted but weren't|
|M6|`numAllocaOriginInnerLoopAccesses`|Memory|**Semantic**|Thread-local data access in hot loops|
|M7|`numArgOriginInnerLoopAccesses`|Memory|**Semantic**|Opaque pointer access in hot loops|
|M8|`numNoAliasArguments`|Memory|**Semantic**|Alias information available to compiler|
|M9|`numGEPsWithMultipleIndices`|Memory|Structural|Multi-dimensional access complexity|
|M10|`numMemcpyToAlloca`|Memory|**Semantic**|Data localization (closure copy pattern)|
|P1|`numFloatArithmeticInsts`|Compute|Structural|FP compute volume|
|P2|`numIntegerArithmeticInsts`|Compute|Structural|Integer compute (often overhead)|
|P3|`numMulFeedingAdd`|Compute|**Semantic**|FMA opportunity count|
|P4|`numReductionPHIs`|Compute|**Semantic**|Successful reduction recognition|
|P5|`numContractFlaggedFPOps`|Compute|**Semantic**|FP fusion eligibility|
|P6|`numFastMathFPOps`|Compute|**Semantic**|Compiler's FP optimization freedom|
|P7|`numInnerLoopFPOps`|Compute|Structural|Hot-path compute intensity|
|P8|`numIntegerMulsInGEPChains`|Compute|**Semantic**|Address computation overhead|
|P9|`numCastInsts`|Compute|Structural|Type conversion overhead|
|P10|`numCallsToMathFunctions`|Compute|Structural + Semantic|Expensive math operation count|

Polybench_ADI: Why RAJA is 50% slower

|Root Cause|Metric Signal|Impact|
|---|---|---|
|**No store forwarding** — RAJA loads P[j-1] and Q[j-1] from global memory every iteration; Native forwards them through register PHIs|**M4**: 2 → 0 (promoted loads)|**2 extra global memory loads per iteration** of the j-loop — on GPU, global memory latency is ~400 cycles|
|**Loop-invariant branch inside loops** — RAJA re-checks thread bounds every iteration, which both wastes a cycle and prevents the compiler from recognizing the store-forwarding pattern|**C7**: 0 → 2 (invariant branches in loops)|Blocks store forwarding, blocks loop versioning, adds branch overhead|
|**No loop versioning** — Native generates a runtime alias check and an optimized loop; RAJA can't because the invariant branch prevents the analysis|**C3**: 3 → 2 (loops)|Prevents the optimization that enables store forwarding|
|**More integer overhead** — RAJA computes strided loop trip counts with sdiv/freeze/rem and has more stride multiplications|**P2**: 22 → 28, **P8**: 6 → 10|Additional ALU overhead for address computation|
|**More closure loads at entry** — RAJA loads ~27 values from the constant-memory closure struct|**M1**: 18 → 33|One-time cost, but increases register pressure|
