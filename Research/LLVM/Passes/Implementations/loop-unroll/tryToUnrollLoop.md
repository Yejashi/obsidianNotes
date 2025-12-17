

#### Structural Requirements

```
if (!L->isLoopSimplifyForm())
  return Unmodified;
```
The loop must be in LoopSimplify form, where it it has:
- Single preheader
- Single latch
- Canonical exits

#### Gather unrolling + peeling preferences

This merges:
- Opt level (`-O1/-O2/-O3`)
- Loop metadata
- **Command-line overrides**:
    - `-unroll-count`
    - `-unroll-threshold`
    - `-unroll-runtime`
    - `-unroll-allow-partial`
    - `-unroll-max-count`
    - etc.

