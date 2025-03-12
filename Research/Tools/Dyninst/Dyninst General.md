### Introduction

The typical software development cycle consists of editing source code, compiling it, and executing the resulting binary. However, in certain situations, this cycle is restrictive. The ability to modify a program while it is running or after it has been linked allows for more flexibility by avoiding the need for recompilation, relinking, or restarting execution.

Some practical applications for modifying running programs include:

- **Performance Analysis**: Adding instrumentation to a running application to diagnose performance bottlenecks.
- **Performance Steering**: Modifying large-scale simulations dynamically to adjust computations or data.
- **Debugging**: Making real-time changes to track or fix issues without restarting execution.
- **Application Composition**: Dynamically altering or extending software functionalities.

The **DyninstAPI** provides an interface to insert code into either a running application (dynamic instrumentation) or a binary on disk (static instrumentation). This API allows for:

- Inserting and modifying instrumentation in a running program.
- Inserting instrumentation into an on-disk binary and writing a modified version to disk.
- Performing static and dynamic analysis on binaries and processes.

The API aims to provide a **machine-independent interface** for runtime and static code patching while remaining simple and expressive.

---

### Abstractions in DyninstAPI

DyninstAPI is structured around key abstractions for working with program binaries and processes:

1. **Mutator and Mutatee**:
    - The **mutator** is the process that uses DyninstAPI to modify an application.
    - The **mutatee** is the application being modified (either a running process or an on-disk binary).
2. **Instrumentation Points and Snippets**:
    - A **point** is a location in a program where instrumentation can be inserted (e.g., function entry points).
    - A **snippet** is an executable code segment to be inserted at a specified point (e.g., incrementing a counter).
3. **Address Space Abstraction**:
    
    - Represents processes (for dynamic instrumentation) or binaries (for static instrumentation).
    - Extends to include:
        - **Process abstraction**: Captures runtime details like threads and stack state.
        - **Binary abstraction**: Represents on-disk executables and their dependencies.
4. **Function and Variable Abstractions**:
    
    - Functions contain **points** for inserting instrumentation.
    - Functions also include **control flow graph** (CFG) details such as loops, basic blocks, and edges.
    - If debug information is available, additional details such as function parameters, variable types, and source code lines are accessible.
    - The complete set of functions and variables in a mutatee is called an **image**.
5. **Type System**:
    
    - DyninstAPI uses a simple type system based on structural equivalence.
    - If debug symbols are available in a supported format, the API performs type checking on inserted code.
6. **Handling Function Overlap**:
    
    - Due to compiler optimizations, multiple functions may share code or have multiple entry points.
    - DyninstAPI treats each function (`BPatch_function`) as having a single entry point.
    - Ensures that inserted instrumentation executes only within its designated function context.

---

### Examples of DyninstAPI Usage

To illustrate how DyninstAPI is used, here are basic examples of function instrumentation:

#### 1. Setting Up a Mutator

A mutator program starts by creating an instance of the `BPatch` class, which provides global access to DyninstAPI functionalities:

```cpp
BPatch bpatch;
```

Instrumentation is done through a `BPatch_addressSpace` object, which allows operations on both running processes and on-disk binaries:

- **Attaching to a Running Process**:
    
    ```cpp
    BPatch_process *appProc = bpatch.processAttach(name, processId);
    ```
    
    This creates an instance of `BPatch_process` that references an existing process.
    
- **Creating a New Process for Instrumentation**:
    
    ```cpp
    BPatch_process *appProc = bpatch.processCreate(pathname, argv);
    ```
    
    This starts a new process with instrumentation capabilities.
    
- **Opening an On-Disk Binary for Static Instrumentation**:
    
    ```cpp
    BPatch_binaryEdit *appBin = bpatch.openBinary(pathname);
    ```
    
    This allows modifications to an executable before execution.
    

Since `BPatch_process` and `BPatch_binaryEdit` both inherit from `BPatch_addressSpace`, they can be cast as needed:

```cpp
BPatch_addressSpace *app = static_cast<BPatch_addressSpace *>(appProc);
```

#### 2. Finding a Function Entry Point for Instrumentation

To insert instrumentation at a function's entry point:

```cpp
std::vector<BPatch_function *> functions;
std::vector<BPatch_point *> *points;
BPatch_image *appImage = app->getImage();
appImage->findFunction("InterestingProcedure", functions);
points = functions[0]->findPoint(BPatch_locEntry);
```

Here:

- `findFunction` retrieves the function named _InterestingProcedure_.
- `findPoint(BPatch_locEntry)` gets the function's entry point.

#### 3. Inserting an Instrumentation Snippet

To insert a snippet that increments a counter:

```cpp
BPatch_variableExpr *intCounter = app->malloc(...);
BPatch_arithExpr incExpr(BPatch_assign, *intCounter, BPatch_arithExpr(BPatch_plus, *intCounter, BPatch_constExpr(1)));
BPatch_snippet *instrumentation = new BPatch_snippet(incExpr);
app->insertSnippet(*instrumentation, *points);
```

- `malloc(...)` allocates a variable in the mutatee to store the counter.
- `BPatch_arithExpr` constructs an expression that increments the counter.
- `insertSnippet` inserts the code at the specified instrumentation points.

---

### Summary

DyninstAPI provides a powerful way to insert and modify code in running applications or static binaries. Its key features include:

- Dynamic and static instrumentation.
- Process and binary abstractions.
- Fine-grained control over function and variable instrumentation.
- Type-aware code insertion when debugging symbols are available.

By leveraging DyninstAPI, users can perform advanced debugging, performance analysis, and runtime application modifications efficiently.