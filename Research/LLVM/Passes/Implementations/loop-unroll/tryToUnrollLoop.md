Source: https://llvm.org/doxygen/LoopUnrollPass_8cpp_source.html

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

#### Early exit: unrolling disabled by thresholds
```
if (UP.Threshold == 0 &&
    (!UP.Partial || UP.PartialThreshold == 0) &&
    !OptForSize)
  return Unmodified;
```

#### Ephemeral values + cost modeling
```
collectEphemeralValues(...)
UCE.canUnroll()
```
- Ephemeral values = short-lived temps that **should not count heavily** toward code size
- If the loop:
    - Has irreducible CFG
    - Has unsafe instructions
    - Has disallowed side effects


#### Loop size & opt-for-size adjustment
```
LoopSize = UCE.getRolledLoopSize();
if (OptForSize)
  UP.Threshold = max(UP.Threshold, LoopSize + 1);
```

#### Inlinable calls block unrolling
