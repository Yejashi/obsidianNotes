

#### Structural Requirements

```
if (!L->isLoopSimplifyForm())
  return Unmodified;
```
The loop must be in LoopSimplify form, where it it has:
- Single preheader
- Single latch
- Canonical exits

#### 
