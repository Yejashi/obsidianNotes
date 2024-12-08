### [Writing LLVM Pass in 2018 — Part I](https://medium.com/@mshockwave/writing-llvm-pass-in-2018-part-i-531c700e85eb)
When creating a pass you inherit from one of two classes:
- `llvm::PassInfoMixin`: for transformation passes.
- `llvm::AnalysisInfoMixin`: for analysis passes.

#### TODO: RENAME LATER
```cpp
struct HelloNewPMPass : public PassInfoMixin<HelloNewPMPass> {
  PreservedAnalyses run(Function &F, FunctionAnalysisManager &FAM) {
    return PreservedAnalyses::all();
  }
};
```