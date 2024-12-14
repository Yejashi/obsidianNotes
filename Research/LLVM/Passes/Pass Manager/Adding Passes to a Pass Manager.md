To [add a pass](https://llvm.org/docs/NewPassManager.html) to a new PM pass manager, the important thing is to match the pass type and the pass manager type. 

For example, a FunctionPassManager can only contain function passes:
```cpp
FunctionPassManager FPM;
// InstSimplifyPass is a function pass
FPM.addPass(InstSimplifyPass());
```

If you want to add a loop pass that runs on all loops in a function to a FunctionPassManager, the loop pass must be wrapped in a function pass adapter that goes through all the loops in the function and runs the loop pass on each one.

```cpp
FunctionPassManager FPM;
// LoopRotatePass is a loop pass
FPM.addPass(createFunctionToLoopPassAdaptor(LoopRotatePass()));
```

The IR hierarchy in terms of the new PM is Module -> (CGSCC ->) Function -> Loop, where going through a CGSCC is optional.

```cpp
FunctionPassManager FPM;
// loop -> function
FPM.addPass(createFunctionToLoopPassAdaptor(LoopFooPass()));

CGSCCPassManager CGPM;
// loop -> function -> cgscc
CGPM.addPass(createCGSCCToFunctionPassAdaptor(createFunctionToLoopPassAdaptor(LoopFooPass())));
// function -> cgscc
CGPM.addPass(createCGSCCToFunctionPassAdaptor(FunctionFooPass()));

ModulePassManager MPM;
// loop -> function -> module
MPM.addPass(createModuleToFunctionPassAdaptor(createFunctionToLoopPassAdaptor(LoopFooPass())));
// function -> module
MPM.addPass(createModuleToFunctionPassAdaptor(FunctionFooPass()));

// loop -> function -> cgscc -> module
MPM.addPass(createModuleToPostOrderCGSCCPassAdaptor(createCGSCCToFunctionPassAdaptor(createFunctionToLoopPassAdaptor(LoopFooPass()))));
// function -> cgscc -> module
MPM.addPass(createModuleToPostOrderCGSCCPassAdaptor(createCGSCCToFunctionPassAdaptor(FunctionFooPass())));
```

A pass manager of a specific IR unit is also a pass of that kind. For example, a `FunctionPassManager` is a function pass, meaning it can be added to a `ModulePassManager`:
```
```