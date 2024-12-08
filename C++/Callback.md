In C++, a callback is a function that is passed as an argument to another function, which then calls (or "invokes") it at some later time. 

The idea is that the function receiving the callback can execute the provided function at a specific point during its execution, allowing the calling code to provide custom behavior.

There are a few common ways to implement callbacks in C++:
**Function Pointers:**
```cpp
#include <iostream>

// A simple callback function
void callbackFunction() {
    std::cout << "Callback function executed!" << std::endl;
}

// A function that accepts a callback function
void executeCallback(void (*callback)()) {
    std::cout << "Before callback." << std::endl;
    callback();  // Call the passed-in function
    std::cout << "After callback." << std::endl;
}

int main() {
    executeCallback(callbackFunction);  // Pass the function as a callback
    return 0;
}
```

...

[TODO]
### Callbacks in LLVM

In the context of LLVM pass instrumentation, a callback can be thought of as a mechanism that allows you to insert custom behavior into the LLVM optimization or transformation pipeline.

This is achieved by passing a function (or an object) that gets invoked at specific points during the execution of an LLVM pass.

When writing custom LLVM passes, you often need to define specific actions that occur at certain stages of the pass (e.g., when visiting a function, instruction, or basic block). Callbacks provide a flexible way to define those actions, often by letting you inject code that will be executed at predefined points.