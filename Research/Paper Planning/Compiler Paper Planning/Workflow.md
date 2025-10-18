
## General Workflow

### Step 1 — **Runtime instrumentation (Caliper, Thicket, etc.)**
Collect:
- Region-level wall time, GPU time, and PAPI counters
- Metadata (kernel name, function name, source line)
These tell me _“what ran and how long it took.”_

### Step 2 — **Compiler optimization remarks**
These tell me _“what the compiler did to this code.”_

### Step 3 — **Correlate by region**
Map Caliper regions ↔ source lines ↔ remark entries.  
That lets me ask:
> “This region got faster from -O2→-O3; what new remarks appeared or disappeared?”

### Step 4 — **Hypothesis building**
From that correlation i hypothesize:
- “Vectorization remark appeared → likely SIMD speedup.”
- “Loop unrolled → maybe higher register pressure.”
- “No remark change but runtime changed → backend or hardware effect.”
    

---

##  When i need to _go deeper_

Once a hypothesis looks interesting (“why did -O3 slow down this region?”), i descend the stack:

| Layer                             | What i inspect                                                                                        | Purpose                                                        | Machine-readable options                                                  |
| --------------------------------- | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **LLVM IR diffs**                 | Output from `opt -S -print-changed` or `-fpass-plugin=PrintFunction`                                  | See structural change (loop deleted, inlined, etc.)            | Use `-print-changed-format=json` (LLVM ≥17) — gives structured JSON diffs |
| **Optimization pass trace**       | `-debug-pass-manager` logs                                                                            | See which passes actually ran and in what order                | Parse textual trace or use `opt --print-pipeline-passes`                  |
| **Machine code / scheduling**     | `llvm-mca`, `llvm-objdump -d`, `-fsave-optimization-record -fsave-optimization-record-passes=machine` | Verify instruction mix, register pressure                      | `llvm-mca` JSON output gives IPC, bottlenecks                             |
| **Hardware performance counters** | Caliper, HPCToolkit, perf, rocprof                                                                    | Validate whether hypothesis holds (cache misses, stalls, etc.) | All export CSV/JSON                                                       |
| **Debug metadata linkage**        | `llvm-dwarfdump`, DWARF line tables                                                                   | Re-link machine code to source for region correlation          | Dwarf4/5 line info in binary, can parse via `pyelftools`                  |

By connecting these layers via `DebugLoc` or DWARF line info, i can make the “why” traceable.

---
## Making it machine-readable

LLVM already gives me structured outputs at multiple levels:

| Artifact                         | Flag / tool                                      | Format           | Notes                               |
| -------------------------------- | ------------------------------------------------ | ---------------- | ----------------------------------- |
| **Optimization remarks**         | `-fsave-optimization-record                      | json             | YAML/JSON                           |
| **Pass diffs**                   | `opt -print-changed-format=json`                 | JSON             | Gives before/after IR for each pass |
| **Machine performance analysis** | `llvm-mca -output=json`                          | JSON             | Static throughput/latency model     |
| **Caliper data**                 | `cali-query --format json`                       | JSON             | Region metrics                      |
| **Binary-level info**            | `llvm-objdump --source --demangle --disassemble` | text (parseable) | Map instructions back to lines      |
   
---

## . What this buys me

I get a _progressive analysis model_:

| Layer                       | Question answered                         |
| --------------------------- | ----------------------------------------- |
| **Caliper runtime data**    | “Which region is slow?”                   |
| **Remarks**                 | “What optimizations did LLVM apply here?” |
| **IR diff**                 | “How did the code structure change?”      |
| **Machine code / counters** | “Did that change actually help or hurt?”  |
And i only pay the cost of deeper introspection for the regions that look suspicious or interesting.

***
## Example workflow


## 🧩 1. Start: the high-level _observation_

You have **measured runtime** for your app or region — say:

| Opt level | Runtime (ms) |
| --------- | ------------ |
| -O0       | 4.8          |
| -O3       | 0.02         |

Your first goal isn’t to explain every micro-optimization — it’s to _narrow down what changed semantically_.

So you start from the **performance delta**:

> “The region got ~200× faster.”

---

## 🧠 2. Correlate with **remarks**

Now bring in your optimization remarks:

```
Loop deleted because it is invariant [-Rpass=loop-delete]
'_ZL3foov' not inlined because of noinline
marked as tail call candidate
```

At this level, remarks act like _semantic breadcrumbs_.  
They let you hypothesize:

|Remark|Possible performance meaning|
|---|---|
|`loop deleted`|Entire loop computation constant-folded away → huge static simplification.|
|`not inlined`|Function call remains → minor, predictable overhead.|
|`tail call`|Call frame reused → negligible extra cost.|

So your initial hypothesis is simple:

> “The loop was deleted because the compiler proved its effect is constant, reducing the function to a constant return.”

This explains _qualitatively_ why performance improved.

---

## ⚙️ 3. Verify by looking at the **optimized IR**

Now you want to confirm whether your hypothesis is true.

**Command:**

```bash
clang -O3 -emit-llvm -S source.c -o opt.ll
```

Inspect `foo()` in `opt.ll`.

You’ll likely see:

```llvm
define dso_local i32 @foo() {
entry:
  ret i32 10
}
```

So indeed:

- Loop and arithmetic are gone.
    
- Function just returns a constant.
    

This confirms _structural elimination_ → zero runtime work.

---

## 🧮 4. Reconnect to **pass history**

If you log the pipeline (e.g., with `-debug-pass-manager`), you’ll see:

```
SimplifyCFGPass
SROAPass
InstCombinePass
IndVarSimplifyPass
LoopDeletionPass
SimplifyCFGPass
```

The reasoning chain is now explicit:

1. **SROA / InstCombine** → exposed that all ops are pure integer math.
    
2. **IndVarSimplify** → proved loop trip count fixed and body side-effect-free.
    
3. **LoopDeletion** → removed the loop.
    
4. **SimplifyCFG** → cleaned up dead code.
    

→ Therefore, “loop deleted because it is invariant” isn’t arbitrary — it’s the _consequence_ of those transformations.

---

## 🔬 5. If you want to quantify _impact_, go down another layer

You can now connect:

- **Before/after IR** (`-print-changed-format=json`)
    
- **Assembly** (`llvm-objdump -d`)
    
- **Runtime measurement (Caliper)**
    

and demonstrate:

|Level|Before|After|
|---|---|---|
|IR|10-iteration loop|`ret i32 10`|
|ASM|~30 instructions|1 `mov`, 1 `ret`|
|Runtime|~4.8 ms|~0.02 ms|

Now you can write the full explanation:

> “Between -O0 and -O3, LLVM identified that the loop in `foo()` had a fixed trip count and side-effect-free body. Through scalar replacement and induction variable simplification, it proved the final value was constant. `LoopDeletionPass` eliminated the loop, reducing the function to a constant return. This removed all iteration overhead, explaining the 200× speedup. The remarks corroborate this (`loop deleted`, `tail call candidate`).”

---

## 🧠 6. General method — “Top-down explanation pipeline”

Here’s the repeatable workflow you can apply to any region:

|Step|Question|Artifact|Tool|
|---|---|---|---|
|1|What changed in runtime?|Performance metrics|Caliper, Thicket|
|2|What optimizations fired?|Optimization remarks|`-fsave-optimization-record`|
|3|What structural code change occurred?|IR diff|`opt -print-changed-format=json`|
|4|What caused it?|Pass trace|`-debug-pass-manager`|
|5|Did it help?|Runtime + hardware counters|Caliper, perf, HPCToolkit|

Each level either _confirms_ or _refines_ your hypothesis.

---

## ✅ 7. TL;DR — in your example

|Level|Evidence|Conclusion|
|---|---|---|
|Performance|Runtime collapsed|Something got constant-folded|
|Remarks|`loop deleted because it is invariant`|Compiler proved loop redundant|
|IR|`ret i32 10`|Loop fully replaced by constant|
|Pass sequence|SROA → InstCombine → IndVarSimplify → LoopDeletion|Causal chain established|
|Assembly|1 `mov`, 1 `ret`|Minimal instruction count|
|Runtime|200× faster|Optimization fully explains behavior|

---

So your **top-down reasoning** looks like:

> **Observation:** Function runs faster.  
> **Clue:** “Loop deleted because it is invariant.”  
> **Verification:** Optimized IR shows constant return.  
> **Explanation:** Earlier passes made loop provably invariant; LoopDeletion removed it.  
> **Result:** Constant folding → no runtime loop → major speedup.

That’s the ideal structured analysis loop (no pun intended) — remarks guide your _hypothesis_, IR and pass data provide the _mechanistic explanation_, and runtime metrics confirm the _effect_.