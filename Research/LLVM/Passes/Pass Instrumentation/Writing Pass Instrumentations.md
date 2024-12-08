See [[Pass Instrumentations]] for general information.


### Recap on how to write a pass plugin
See [[Writing an LLVM Pass]] for more general information.

Let's begin with “plugin entry point”, or the registration callback in the Pass plugin:
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

The lambda function from line 5 to 7 gives you a PassBuilder instance which you can use to register your Pass at a desired position in the Pass pipeline. 

### Registering a new Pass Instrumentation
Let’s create a simple demo mimicking the functionality of `-stop-after` command line option, which effectively stalls the entire pass pipeline after finishing the designated pass.

