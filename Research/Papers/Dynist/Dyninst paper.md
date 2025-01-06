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

Our CFG is based on five abstractions: the **inter-procedural control flow graph** (consisting of **basic blocks** and **edges**), **functions**, and **loops**.

We also define instrumentation points (or instpoints) for each of these abstractions, which identify locations where instrumentation can be inserted, and code snippets, which represent the inserted instrumentation code.

An instpoint is a simple abstraction; when the point is reached during execution, the instrumentation at that point executes. 
- An instpoint is an annotation of a subgraph of the CFG.

We define two classes of instpoints; **augmentation** and **transformation** instpoints.
- An **augmentation instpoint**, such as pre-instruction or block entry, adds additional code to an existing basic block rather than transforming the CFG. 
- **Transformation instpoints**, (e.g., function entry or edge instpoints) insert instrumentation by adding new blocks and edges to the CFG.
	- We define the following transformation instpoints: function entry and exit; loop entry, exit, beginning of iteration, and end of iteration; block exit; and edge.

Edges are labeled with an edge type.

We define the following types: direct, fallthrough, conditional taken, conditional not taken, indirect, call, call fallthrough, and return, where call fallthrough edges link blocks ending with calls to their intraprocedural successors. 

An edge is interprocedural if it **leaves a function** and intraprocedural otherwise.

We define a **function** as the blocks reachable from an entry block traversing **only intraprocedural edges**. 

We use **natural loops** for our loop definition.
- A natural loop is the set of basic blocks that form a cycle in the CFG, with a specific entry point called the **loop header**.
- Natural loops are defined based on back edges and the dominance relationship between basic blocks.

#### Complicating Cases
There are some code structures common in binaries that can complicate the mapping of control flow abstractions onto the binary code. Dyninst aims to hide these complexities as much as possible from the user.

We handle two cases: **Overlapping Basic Blocks** and **Overlapping Functions**

Overlapping basic blocks occur when the same sequence of bytes disassembles to two distinct instruction sequences, both of which may be executed by the program.
- Overlapping basic blocks in the context of control flow graphs (CFGs) occur when a basic block belongs to multiple regions or structures, such as multiple loops. 
- This situation typically arises in nested or overlapping control structures in the source code, where the same block can serve different roles in different contexts.
- ```while (condition1) {
    if (condition2) {
        do_work1();
    }
    do_work2();
}```

Overlapping functions occur when multiple functions include the same basic block. We represent this sharing in our interprocedural CFG, but hide it at the function layer by using block aliases.

A block alias represents a shared block in the context of one particular function, and any analysis or instrumentation performed on the alias is restricted to that function.

#### Generating Instrumented Code
The final step required for anywhere instrumentation is to generate new code from the instrumented CFG.

The annotations represented by instpoints cannot be directly used to generate code. 

Instead, we first construct an **augmented CFG** that represents the instrumented code, and this augmented CFG is then used to generate the new instrumented binary code.

We generate the augmented CFG in two steps:
- First, we use block cloning to convert all instrumented block aliases to actual blocks, which eliminates sharing of instrumented code.
- Second, we apply the appropriate graph transformation rule for each instpoint to insert the appropriate code snippets into the graph.

The resulting augmented CFG is used to generate code with standard code generation techniques.

We then use this graph to generate the actual instrumented code. This requires three things:
- Compiling instrumentation requests into binary code
- Updating original and adding additional control flow instructions to ensure the newly generated code matches the CFG
- Ensuring that original instructions maintain their original behavior

The first two are performed with standard compiler techniques.

### Any Time Instrumentation
The CFG-based instrumentation technique discussed in the previous section generates instrumented code.

In this section, we discuss how we insert this instrumented code into the binary at any time during execution while imposing proportional cost. 

Current patch-based instrumenters impose proportional cost, but are not capable of instrumenting at any time because they cannot insert or modify actively executing code.

We describe two new techniques that address this lack:
- **State interception:** directly modifies process state to allow instrumenting executing code.
- **Iterative Instrumentation:** provides the ability to modify or remove instrumentation at any point during execution.

#### Instrumentation Overview
Binaries rarely include sufficient space to insert instrumentation without moving original code. 

Instead, instrumenters create a copy of this code that is instrumented and then execute the copied code in place of the original. This code is copied using a technique we call relocation. 
- Relocating a region of code produces a new version that emulates the behavior of the original code, but contains sufficient space to insert instrumentation.

Once a region of code has been relocated, the instrumenter must ensure it is executed in place of the original code. This is done with one of two methods:
- **Path-Based Instrumentation** overwrites the original code with interception branches to the relocated code.
- **JIT Instrumentation** instead relocates all code as it is executed. This approach does not modify original code but imposes relocation overhead on all code rather than just instrumented code, and thus **does not impose proportional cost**.

Patch-based instrumentation operates in three phases:
- **Selection Phase**: selects the code that will be relocated and patched; we refer to this code as the selected code.
- **Relocation Phase:** creates a copy of the code selected in the previous phase; we then use the techniques described in Section 2 to add instrumentation to this region and copy the resulting code into the binary
- **Patching Phase:** patches the binary with interception branches that will jump from the selected region to the relocated region.
	- Redirect execution from the original code to the relocated and instrumented code


#### State Interception and Iterative Instrumentation
The patch-based algorithm as described above has two weaknesses.
- First, it does not support instrumenting programs that are executing inside the selected region, since it only inserts interception branches at the boundaries of this region.
	- If a program is already running inside the selected region when instrumentation begins the original code continues executing as the interception branches only apply at entry/exit points.
- Second, it does not support modifying previously inserted instrumentation if the program is executing inside the instrumented region.
	- Once instrumentation is applied and the program is running in the instrumented region, the patch-based algorithm struggles to make further changes to the instrumentation.
	- This is because modifying instrumentation mid-execution can cause conflicts, such as disrupting the program’s state or flow.

We present two techniques, **state interception** and **iterative instrumentation**, that address these problems.
- State Interception:
	- This involves modifying the state of a program while it is running, specifically moving the program's execution from the current point to a predetermined location in the instrumentation code.
	- This is done by directly changing the execution context of the program's threads instead of adding a conditional branch instruction.
- Iterative Instrumentation:
	- Iterative instrumentation allows a user to further instrument previously instrumented code or remove instrumentation at any time.
	- Three Step Process:
		- Generate a New Version of Instrumentation by applying a patch based algorithm.
		- Redirect to the New Version by 
		- 
