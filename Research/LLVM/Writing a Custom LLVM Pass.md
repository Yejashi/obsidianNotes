### Define the pass
To write a pass, you need to subclass the appropriate pass class depending on whether you want to perform an analysis or a transformation.

For example, if you want to create a function pass, you’ll subclass `FunctionPass`. Consider the following example:
```cpp
#include "llvm/Pass.h"
#include "llvm/IR/Function.h"
#include "llvm/IR/Module.h"
#include "llvm/IR/IRBuilder.h"
#include "llvm/Support/raw_ostream.h"

using namespace llvm;

namespace {
  // Define the pass as a subclass of FunctionPass
  struct TrackOptimizations : public FunctionPass {
    static char ID; // Unique identifier for the pass
    TrackOptimizations() : FunctionPass(ID) {}

    // The run method is where the pass logic goes
    bool runOnFunction(Function &F) override {
      unsigned optimizationCount = 0; // Counter for optimizations

      // Example optimization: Simplifying arithmetic
      for (auto &BB : F) {
        for (auto &I : BB) {
          if (auto *addInst = dyn_cast<BinaryOperator>(&I)) {
            if (addInst->getOpcode() == Instruction::Add) {
              optimizationCount++; // Count an addition optimization
            }
          }
        }
      }

      // Output the result (number of optimizations performed)
      errs() << "Function " << F.getName() << " had " 
             << optimizationCount << " optimizations.\n";

      return false; // Indicate that the function wasn't modified
    }
  };
}

char TrackOptimizations::ID = 0;
static RegisterPass<TrackOptimizations> X("track-optimizations", 
                                           "Track Optimization Attempts Per Function", 
                                           false, false);

```

