### [Writing LLVM Pass in 2018 — Part I](https://medium.com/@mshockwave/writing-llvm-pass-in-2018-part-i-531c700e85eb)
When creating a pass you inherit from one of two classes:
- `llvm::PassInfoMixin`: for transformation passes.
- `llvm::AnalysisInfoMixin`: for analysis passes.

#### Start of by inheriting the appropriate parent class
```cpp
class HelloNewPMPass : public PassInfoMixin<HelloNewPMPass> {
  PreservedAnalyses run(Function &F, FunctionAnalysisManager &FAM) {
    return PreservedAnalyses::all();
  }
};
```

The `run` method is where the logic for the pass goes as that's what the pass manager calls when it needs to execute the pass.

### 