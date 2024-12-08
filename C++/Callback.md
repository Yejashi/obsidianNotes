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


