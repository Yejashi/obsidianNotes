To [add a pass](https://llvm.org/docs/NewPassManager.html) to a new PM pass manager, the important thing is to match the pass type and the pass manager type. 

For example, a FunctionPassManager can only contain function passes:
```cpp
FunctionPassManager FPM;
// InstSimplifyPass is a function pass
FPM.addPass(InstSimplifyPass());
```

If you want to add a loop pass that runs on all loops in a function to a FunctionPassManager, the loop pass must be wrapped in a function pass adaptor that goes through all the loops in the function and runs the loop pass on each one.