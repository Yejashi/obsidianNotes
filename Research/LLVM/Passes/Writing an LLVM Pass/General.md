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

#### Then register the pass
```cpp
extern "C" ::llvm::PassPluginLibraryInfo LLVM_ATTRIBUTE_WEAK
llvmGetPassPluginInfo() {
  return {
    LLVM_PLUGIN_API_VERSION, "HelloNewPMPass", "v0.1",
    [](PassBuilder &PB) {...}
  };
}
```

The curly brackets after `return` statement would construct a `llvm::PassPluginInfo` object, carrying some Pass information.

The last field, a lambda function, is provided with a `PassBuilder` instance.

`PassBuilder`, as its name revealed, is used to build the PassManager pipeline. So we’re going to use it to “insert” our Pass into a proper place inside the pipeline.

```cpp
extern "C" ::llvm::PassPluginLibraryInfo LLVM_ATTRIBUTE_WEAK
llvmGetPassPluginInfo() {
  return {
    LLVM_PLUGIN_API_VERSION, "HelloNewPMPass", "v0.1",
    [](PassBuilder &PB) {
      PB.registerPipelineParsingCallback(
        [](StringRef PassName, FunctionPassManager &FPM, ...) {
          if(PassName == "hello-new-pm-pass"){
            FPM.addPass(HelloNewPMPass());
            return true;
          }
          return false;
        }
      );
    }
  };
}
```

There is, `registerPipelineParsingCallback`, where you can register a callback that is invoked when a pass name is parsed from the textual description.

Therefore, we can run our pass with `opt` command similar to the below:
```bash
opt -passes="hello-new-pm-pass" ...
```


