### [Writing LLVM Pass in 2018 — Part I](https://medium.com/@mshockwave/writing-llvm-pass-in-2018-part-i-531c700e85eb)
When creating a pass you inherit from one of two classes:
- `llvm::PassInfoMixin`: for transformation passes.
- `llvm::AnalysisInfoMixin`: for analysis passes.

