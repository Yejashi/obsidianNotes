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

The lambda function from line 5 to 7 gives you a `PassBuilder` instance which you can use to register your Pass at a desired position in the Pass pipeline. 

### Registering a new Pass Instrumentation
Instrumentation allows you to observe or modify the behavior of passes during their execution.

In this example, a class `StopAfterInstrument` is created to mimic the `-stop-after` command-line option, which stops the pipeline after a specific pass is executed.

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

This will register the `beforePass` and `afterPass` function in the same class as the callbacks invoked before and after each Pass, respectively.

Though function prototypes of these two callback have same argument types, the return types are different:
- The first argument represents the textual `Pass Id`.
- The second argument is the input IR, represented in `llvm::Any` type.

For callbacks running before a Pass (i.e. the callback for `registerBeforePassCallback`), the returned boolean indicating whether `PassManager` should run this Pass or not.


```cpp
void registerCallbacks(PassInstrumentationCallbacks& PIC) {
  using namespace std::placeholders;
  PIC.registerBeforePassCallback(
    std::bind(&StopAfterInstrument::beforePass, this, _1, _2));
  PIC.registerAfterPassCallback(
    std::bind(&StopAfterInstrument::afterPass, this, _1, _2));
}
```
- The `registerCallbacks` method registers the callbacks (`beforePass` and `afterPass`) to be called at the appropriate times (before and after a pass runs).
- **`PassInstrumentationCallbacks`** is an object that allows you to hook into the pass pipeline to insert custom behavior. It provides methods like `registerBeforePassCallback` and `registerAfterPassCallback`.
	- `registerBeforePassCallback`: Registers the `beforePass` callback to be called before a pass runs.
	- `registerAfterPassCallback`: Registers the `afterPass` callback to be called after a pass runs.
- **`std::bind`** is used to bind the member functions (`beforePass` and `afterPass`) to the current instance (`this`) of the `StopAfterInstrument` class, making them callable as regular functions.
	- The `_1` and `_2` are placeholders that represent the arguments passed to the callbacks (`PassID` and `IR`), and they will be substituted when the callback is invoked.

```cpp
static StopAfterInstrument TheStopAfterInstrument;
```
- This creates a **static instance** of the `StopAfterInstrument` class. 
- The `static` keyword ensures that the instance exists for the lifetime of the program and is only created once. 
- This instance will be used to register the callbacks during the plugin initialization

##### Important Takeaways
- **Purpose:** The `StopAfterInstrument` class is designed to hook into LLVM's pass pipeline by registering **callbacks** that run before and after each pass.
- **Callbacks:** The `beforePass` method is called before a pass starts, and the `afterPass` method is called after a pass finishes. 
	- These methods can be used to perform custom actions, such as logging, timing, or modifying the pass execution behavior.
- **Callback Registration:** The `registerCallbacks` method registers the two callbacks using LLVM's `PassInstrumentationCallbacks`, which allow you to insert your custom behavior into the pipeline.
