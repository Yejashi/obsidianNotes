Source: [Anywhere, Any-Time Binary Instrumentation](https://dl.acm.org/doi/pdf/10.1145/2024569.2024572)

### Abstract
```txt
The Dyninst binary instrumentation and analysis framework
distinguishes itself from other binary instrumentation tools
through its abstract, machine independent interface; its em-
phasis on anywhere, any-time binary instrumentation; and
its low overhead that is proportional to the number of in-
strumented locations. Dyninst represents the program in
terms of familiar control flow structures such as functions,
loops, and basic blocks, and users manipulate these repre-
sentations to insert instrumentation anywhere in the binary.
We use graph transformation techniques to insure that this
instrumentation executes when desired even when instru-
menting highly optimized (or malicious) code that other in-
strumenters cannot correctly instrument. Unlike other bi-
nary instrumenters, Dyninst can instrument at any time in
the execution continuum, from static instrumentation (bi-
nary rewriting) to instrumenting actively executing code
(dynamic instrumentation). Furthermore, we allow users
to modify or remove instrumentation at any time, with such
modifications taking immediate effect. Our analysis tech-
niques allow us to insert new code without modifying unin-
strumented code; as a result, all uninstrumented code exe-
cutes at native speed. We demonstrate that our techniques
provide this collection of capabilities while imposing similar
or lower overhead than other widely used instrumenters.
```

**Key Features of Dyninst**
- **Abstract, Machine-Independent Interface**: Unlike tools tied to specific architectures, Dyninst offers a general interface that works across various machine types.
- **Anywhere, Any-Time Instrumentation**: It can add or modify instrumentation (additional code to analyze or monitor a program) at virtually any point in a program's execution life cycle.
- **Low Overhead**: The performance impact is proportional to the amount of instrumentation added, meaning uninstrumented parts of the program run at native speed.

**Program Representation**
- Dyninst represents a program in terms of familiar structures like **functions**, **loops**, and **basic blocks** (units of code with a single entry and exit point).
- Users can interact with these structures to insert or modify instrumentation code.

**Graph Transformations**
- Dyninst uses advanced **graph transformation techniques** to ensure that the inserted instrumentation works as expected.

**Static and Dynamic Instrumentation**
- **Static Instrumentation**: Modifies the binary before execution (binary rewriting).
- **Dynamic Instrumentation**: Adds or changes instrumentation while the program is running.
- Dyninst allows users to modify or remove instrumentation dynamically, with changes taking effect immediately.

### Introduction
Binary instrumentation is a technique that modifies a binary program, either pre-execution or during execution.

Dyninst distinguishes itself from other instrumenters through its **abstract interface**; its emphasis on **anywhere, any-time (AWAT)** instrumentation; and its low overhead that is **proportional to the number of instrumented locations**. 

Other binary instrumentation approaches allow users to insert instrumentation at instructions or specific types of control flow edges.
- Dyninst allows instrumentation at **functions**, **loops**, and **basic blocks**.

Why is this better?
- Instrumenting instructions or edges is not sufficient to capture program behavior based on structural characteristics such as functions or loops.
- Consider the case of instrumenting the entry of a function; such instrumentation should execute only once per function call.
	- Other binary instrumenters do not directly support instrumenting function entries; instead, users instead instrument the first instruction in the function.
	- However, the first instruction of functions with no preamble code may be executed multiple times per function invocation.
	- Therefore, such instrumentation would execute multiple times per invocation.
- This problem is addressed by allowing users to specify instrumentation locations in terms of the control flow graph (CFG) in addition to at the instruction level. 

Dyninst allows users to insert, remove, or modify instrumentation at any time in the execution continuum: pre-execution (binary rewriting), before code has executed for the first time, r while the instrumented code is currently executing (dynamic instrumentation).

Dyninst imposes **proportional cost** by imposing overhead only when instrumented code is executed; furthermore, removing instrumentation also removes its cost

Binary instrumenters rely on a technique we call **relocation** to insert both instrumentation and any additional infrastructure code the instrumenter requires.
- Relocation moves code to a new location where it can be expanded to include new code (instrumentation and analysis code) and transforms it to preserve its original behavior.
- As a result of this transformation the relocated code frequently executes slower than the original.


### Anywhere Instrumentation

The control flow graph (CFG) is a familiar representation of the structural elements in a program (e.g., functions, loops, and basic blocks) and the relationships between them.

Two challenges:
- We must map reasonable program abstractions onto code that may have been highly transformed due to optimization or obfuscation.
- We must regenerate instrumented code from the instrumented CFG that both preserves the behavior of the original code and executes instrumentation when the user specifies

We begin by defining the basic CFG abstractions used by Dyninst, including **functions**, **loops**, **basic blocks**, and the **instrumentation points** that are used to specify where instrumentation is inserted.
#### Control Flow Abstractions

Our CFG is based on five abstractions: the **inter-procedural control flow graph** (consisting of **basic blocks** and **edges**), functions, and loops.



