See [[Pass Instrumentations]] for general information.


### Recap on how to write a pass plugin
See [[Writing an LLVM Pass]] for more general information.

Let's begin with “plugin entry point”, or the registration callback in the Pass plugin:
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

The lambda function from line 5 to 7 gives you a PassBuilder instance which you can use to register your Pass at a desired position in the Pass pipeline. 

### Registering a new Pass Instrumentation
Let’s create a simple demo mimicking the functionality of `-stop-after` command line option, which effectively stalls the entire pass pipeline after finishing the designated pass.

Here is the first step:
```cpp
namespace {
class StopAfterInstrument {
  bool beforePass(StringRef PassID, Any IR) {
    return true;
  }

  void afterPass(StringRef PassID, Any IR) {
  }

public:
  void registerCallbacks(PassInstrumentationCallbacks& PIC) {
    using namespace std::placeholders;
    PIC.registerBeforePassCallback(
      std::bind(&StopAfterInstrument::beforePass, this, _1, _2));
    PIC.registerAfterPassCallback(
      std::bind(&StopAfterInstrument::afterPass, this, _1, _2));
  }
};
} // end anonymous namespace

static StopAfterInstrument TheStopAfterInstrument;

extern "C" ::llvm::PassPluginLibraryInfo LLVM_ATTRIBUTE_WEAK
llvmGetPassPluginInfo() {
  return {
    LLVM_PLUGIN_API_VERSION, "NewPMStopAfterInstrumentPlugin", "v0.1",
    [](PassBuilder& PB) {
      auto& PIC = *PB.getPassInstrumentationCallbacks();
      TheStopAfterInstrument.registerCallbacks(PIC);
    }
  };
}
```

The above code showed that after getting the `PassInstrumentationCallbacks` object from `PassBuilder``,` we passed it to `StopAfterInstrument::registerCallbacks`.

This will register the `beforePass` and `afterPass` function in the same class as the callbacks invoked before and after each Pass, respectively