See [[Pass Instrumentations]] for general information.


### Recap on how to write a pass plugin
See [[Writing an LLVM Pass]] for more general information.

Let's begin with 
```cpp
extern "C" ::llvm::PassPluginLibraryInfo LLVM_ATTRIBUTE_WEAK
llvmGetPassPluginInfo() {
  return {
    LLVM_PLUGIN_API_VERSION, "MyFancyPass", "v0.1",
    [](PassBuilder& PB) {
      // Your pass pipeline registration logics...
    }
  };
}
```
