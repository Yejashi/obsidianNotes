To [add a pass](https://llvm.org/docs/NewPassManager.html) to a new PM pass manager, the important thing is to match the pass type and the pass manager type. 

For example, a FunctionPassManager can only contain function passes:
```cpp
FunctionPassManager FPM;
// InstSimplifyPass is a function pass
FPM.addPass(InstSimplifyPass());
```

