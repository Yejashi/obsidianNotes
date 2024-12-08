This is arguably one of the most disgusting aspects of C++ i have come across.  Curses to whomever invented this syntax.

```cpp
void registerHelloWorldPass(PassBuilder &PB) {
  PB.registerPipelineParsingCallback(
      [](StringRef Name, FunctionPassManager &FPM,
         ArrayRef<PassBuilder::PipelineElement>) {
        // Check if the pass name matches "hello-world"
        if (Name == "hello-world") {
          FPM.addPass(HelloWorld()); // Add the HelloWorld pass to the pipeline
          return true;              
        }
        return false; // Indicate no match found for this pass
      });
}
```

