
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
