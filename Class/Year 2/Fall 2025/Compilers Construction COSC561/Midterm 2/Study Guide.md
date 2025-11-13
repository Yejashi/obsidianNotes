# Question 1
Use Figure 4.37 and the expression grammar 4.1 to parse the string (id * id) + id using the LR parsing algorithm.

![[Screenshot_20251112_074220.png]]

![[Screenshot_20251112_074723.png]]

![[Pasted image 20251112081241.png]]

# Question 2
Given the following grammar construct the LR(0) sets of items.
![[Screenshot_20251112_081447 1.png]]
![[Pasted image 20251112100317.png]]
# Question 3
![[Pasted image 20251112105123.png]]

# Question 4
Given the following grammar construct the LR(1) sets of items.
![[Pasted image 20251112105949.png]]
![[Pasted image 20251112152046.png]]

# Question 5
Use the grammar and the set of items in the last problem to construct the canonical parsing table
![[Pasted image 20251112155432.png]]


# Question 6
Draw the DAG representation for the following expression (as shown in Figure 6.3). Provide the quadruple, triple and indirect triple representations of the expression.
```
(a ∗ c) + b ∗ (a ∗ c) + b − (a ∗ c)
```

![[Pasted image 20251112173030.png]]
![[Pasted image 20251112175448.png]]

![[Screenshot_20251113_003419.png]]

![[Screenshot_20251113_003500.png]]


# Question 7

Give the three-address code that could be emitted to translate the following assignment statement. However, you may not use array index operations. Assume that a is an integer array with 5 rows and 10 columns. Assume that v is an integer variable and i and j are integer parameters passed to the function. Provide solutions for when 1) the arrays are stored in row major order, and 2) the arrays are stored in column major order.
```
v = a[i][j];
```

Row Major:
```
V = *(base_a + (10 * i + j) * 4)
```

```
t1 = 10 * i
t2 = t1 + j
t3 = t2 * 4
t4 = t3 + base_a
t5 = *t4
```

Columns Major:
```
V = *(base_a + (5 * j + i) * 4)
```

```
t1 = 5 * j
t2 = t1 + i
t3 = t2 * 4
t4 = t3 + base_a
t5 = *t4
```

# Question 8
 Use Figures 6.36 and 6.37 to translate the following statement in two passes (no backpatching).
 ```
 if (x > 10 && y! = 0 || x == y) x = y;
 ```

![[Screenshot_20251113_021554.png]]

![[Screenshot_20251113_021615.png]]

![[Screenshot_20251113_080134.png]]
![[Screenshot_20251113_080206.png]]

# Question 9
Use Figures 6.43 and 6.46 to translate the expression in a single pass (use backpatching). Start outputting the code from address 20.
```
if (x > 10 && y! = 0 || x == y) x = y;
```

![[Screenshot_20251113_021654.png]]

![[Screenshot_20251113_021746.png]]


# Question 10
**(a) Why is bottom-up parsing (with one symbol of lookahead) more powerful than top-down parsing (with one lookahead symbol)?**

Bottom-up (LR) parsers can handle a **larger class of context-free grammars** than top-down (LL) parsers.
-  LL(1) parsers require grammars to be **left-factored and free of left recursion**, which limits their expressiveness.
- LR(1) parsers work **without modifying the grammar**, handling **left recursion and ambiguity resolution** automatically using a deterministic PDA. As such,  LR(1) parsing can recognize more grammars than LL(1)

**(b) Explain the different error recovery strategies.**

**Panic-mode recovery** – Discards input until a synchronizing token is found.
- Then resume parsing
**Phrase-level recovery** – Replace the prefix of the remaining input with some string that will
allow the parser to continue looking for errors.
- Could possible go into an infinite loop
**Error productions** – Augment the grammar for the source language to include
productions for common errors. When the error production is used, an appropriate error diagnostic can be issued.
**Global correction** – The compiler applies a least-cost correction by searching for the smallest change that make the input valid (theoretically ideal but impractical).

**(c) What is the general strategy of panic-mode recovery? What are its main advantages?**
**Strategy:** On detecting an error, the parser discards input symbols until a **synchronizing token** (like `;` or `}`) is reached, then resumes parsing.

Advantages:
- Simple and effective.
- Never enters an infinite loop.
- Allows parsing to continue to find multiple errors in one run.

(**d) Give the advantages and disadvantages of using a three-address form of intermediate representation over a zero-address representation**

| Representation               | Advantages                                                                                                                                                | Disadvantages                                                    |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Three-address code (TAC)** | Explicit operands → easier optimization (e.g., common subexpression elimination), simple mapping to machine instructions, supports quadruples/triples/SSA | Consumes more temporaries and storage                            |
| **Zero-address (postfix)**   | Compact (good for stack machines), no explicit operands                                                                                                   | Harder to optimize or perform code motion; implicit dependencies |

**(e) Describe the three strategies to translate large switch statements. What are the characteristics of each approach.**
- **Sequential comparisons:**
    - Series of `if ... goto` tests for each case.
    - **Simple** to generate, but **O(n)** time.
- **Binary decision tree:**
    - Organizes case values hierarchically (binary search).
    - **O(log n)** time; efficient for **sparse** case values.
	- User if
		- Case not dense
- **Jump table:**
    - Builds a **table of case labels** indexed by expression value.
    - **O(1)** dispatch; best for **dense, contiguous** case ranges.
    - Requires extra data space.
    - Use if
	    - Case is dense

**(f) What is static checking? Why is static checking preferable to dynamic checking?**

**Static checking:** Detects errors at **compile time** (type, flow, name, uniqueness).
**Dynamic checking:** Performed at **runtime** (e.g., array bounds)
Preferable because:
- Errors are caught before program execution or distribution.
- Eliminates runtime overhead.
- Increases program reliability and portability.

**(g) Describe the rules for type checking.**
- Operators must be applied to compatible operand types.
- Assignment types must match or be coercible.
- Control expressions (`if`, `while`) must be Boolean.
- Function calls must have correct number and types of parameters.  

**(h) What is coercion, overloading, and polymorphism? Give an example of each in the C language.**

| Concept          | Definition                                       | Example in C                                                                        |
| ---------------- | ------------------------------------------------ | ----------------------------------------------------------------------------------- |
| **Coercion**     | Implicit type conversion by compiler             | `float f = 3;` → integer `3` coerced to `3.0`                                       |
| **Overloading**  | One operator or function used for multiple types | `+` used for both `int` and `float`                                                 |
| **Polymorphism** | Same interface works with multiple data types    | Function-like macros or function pointers (e.g., `qsort()` callback), c++ templates |

Polymorphism
- define routine once but it can be called miltipole times with different values
- printf, since variadic

overloading
- one operator or function used for multiple types
- defining the same function with different parameters
- addition is overloaded

**(i) Understand the purpose of the backpatch routine in the csem assignment.**
**Backpatching** fills in **unresolved jump targets** in control flow constructs during intermediate code generation.

Instead of generating code in two passes, the compiler:
- Emits branch instructions with **placeholder labels**.
- Records them in a **backpatch list**.
- Fills in actual addresses when their target labels are known.

This allows **single-pass code generation** for constructs like `if`, `while`, etc.

**(j) Be able to apply the backpatch routine in a semantic routine for statements such as if, if-else, and while.**

| Construct             | Backpatch Steps                                                                           |
| --------------------- | ----------------------------------------------------------------------------------------- |
| **if (E) S1**         | `backpatch(E.true, S1.begin)`; `backpatch(E.false, next)`                                 |
| **if (E) S1 else S2** | `backpatch(E.true, S1.begin)`; `backpatch(E.false, S2.begin)`; jump end of S1 to after S2 |
| **while (E) S**       | `backpatch(E.true, S.begin)`; `backpatch(S.next, E.begin)`; `backpatch(E.false, next)`    |
Example:
```
if (a < b)
   a = a + 1;
else
   a = a + 2;
```

Generates conditional jumps with true/false lists; backpatch connects them to the correct blocks using `backpatch(e→s_true, m1)` and `backpatch(e→s_false, m2)`

10.1(k) Activation Records and Allocation

An activation record (or stack frame) is a block of storage that holds all the necessary information for a single execution of a procedure, including its parameters, local variables, and return address. Activation records are allocated in different memory regions depending on the language's features:

* Static Data Area: Used by older languages like FORTRAN that do not support recursion. Since only one activation of any function can exist at a time, its memory can be allocated statically at compile time.
* Stack: Used by most conventional languages (C, C++, Pascal). Pushing activation records onto a stack is a natural way to manage nested and recursive function calls.
* Heap: Used by some functional languages. If a local variable needs to persist after its creating function returns (e.g., in a closure), its storage must be allocated on the heap to outlive the function's activation record.

10.1(l) Caller-Save vs. Callee-Save Registers

Registers are partitioned by a calling convention to manage their values across function calls:

* Caller-Save (Scratch) Registers: These registers are not guaranteed to be preserved across a function call. If the caller needs the value in a caller-save register after the function returns, the caller is responsible for saving it to memory before the call and restoring it after.
	- regiesters caller saves that it doesnt want callee to modify
* Callee-Save (Non-scratch) Registers: The value of these registers must be preserved by the called function. If the callee wants to use a callee-save register, it is responsible for saving its original value upon entry and restoring it just before returning to the caller.
	- Registers it saves that the callee assumes the caller doesnt want it to modify
10.1(m) Fields of a General Activation Record

A general-purpose activation record typically contains the following fields:
- local variables, parameters, return value, and the return address

* Actual parameters: Values passed by the caller to the callee.
* Return values: Space for the callee to place its result for the caller.
* Control link: A pointer to the activation record of the caller, used to restore the stack on return.
* Access link: A pointer to access non-local data in lexically scoped languages.
* Saved machine status: Includes the return address and the contents of registers that need to be restored.
* Local data: Storage for variables local to the procedure.
* Temporaries: Space for storing intermediate results of expressions if they cannot be kept in registers.

10.1(n) Conventional vs. VM Runtime Models

* Traditional (C/C++) Model: The compiler translates source code directly into native object code for a specific Instruction Set Architecture (ISA) and Operating System (OS). This code is linked and loaded to be executed directly by the hardware, resulting in high performance but a lack of portability.
* High-Level Language Virtual Machine (Java/Python) Model: The compiler translates source code into a portable, platform-independent format called bytecode, which is a Virtual ISA. This bytecode is then executed by a Virtual Machine (VM) software layer. The VM provides platform independence, as only the VM itself needs to be ported to a new hardware/OS combination.

10.1(o) Features of HLL VM Architectures

High-Level Language VMs provide several important features beyond simple execution:

* Security/Protection: VMs can execute untrusted code in a "sandbox," a restricted environment that prevents it from accessing unauthorized system resources.
* Robustness: Features like automatic memory management (garbage collection) and strong type-checking at runtime prevent common programming errors like memory leaks and type confusion.
* Networking: VMs facilitate incremental loading, where parts of a program (like Java classes) can be loaded over a network on demand, improving startup time.
* Performance: Modern VMs use sophisticated techniques like staged emulation and just-in-time (JIT) compilation to achieve performance competitive with natively compiled code.

10.1(p) Instruction Emulation Techniques

VMs use two primary techniques to execute program instructions (bytecode):

1. Interpretation: The VM reads and executes bytecodes one at a time, translating each into corresponding native machine operations on the fly. This method is simple to implement and has low startup cost but suffers from poor steady-state performance.
2. Binary Translation (JIT Compilation): The VM dynamically translates blocks of frequently executed bytecode into native machine code. This native code is stored in a code cache and executed directly by the hardware on subsequent encounters. JIT compilation has a higher initial cost but provides significantly better performance.

10.1(q) The Ski Rental Problem and Staged Emulation

The ski rental problem is a classic decision problem that serves as an analogy for JIT compilation. A skier must decide each day whether to rent skis for a low daily cost or buy them for a high one-time cost, without knowing how many days they will ski. The optimal strategy is to rent until the total rental cost equals the purchase price, and then buy.

Staged emulation is the solution to this problem in a VM. The VM starts by interpreting a block of code (renting skis). It profiles the code, and once the execution count reaches a certain threshold (the point where the cumulative cost of interpreting equals the cost of compiling), it invokes the JIT compiler to translate the block to native code (buying the skis). This minimizes total execution time by investing in compilation only for "hot" code that will be executed many times.

10.1(r) Code Cache Management Strategies

The code cache is the memory region where a VM stores natively compiled code. Because its size is finite, a strategy is needed for when it becomes full:

* LRU (Least Recently Used) Replacement: Evicts the code block that has not been used for the longest time. While good in theory, this is complex to implement for code caches due to variable-sized blocks and the need to manage backpointers from blocks that jump to the one being evicted.
* Flush When Full: Evicts the entire contents of the cache. This strategy is much simpler to implement, eliminates potentially stale code from previous program phases, and avoids fragmentation. Although it can discard useful code, its simplicity and effectiveness have made it a common choice in practice.

10.1(s) Garbage Collection

Garbage collection (GC) is the process of automatic memory reclamation. The runtime system identifies heap-allocated objects that are no longer accessible by the program and reclaims their storage for future use. An object is considered "garbage" and eligible for collection when there are no live references (pointers) from the program's root set (e.g., global variables, stack variables) pointing to it.

10.1(t) Garbage Collection Strategies

1. Reference Counting:
  * How it works: Each object keeps a count of incoming references. The count is incremented when a new reference is created and decremented when one is destroyed. The object is reclaimed when its count drops to zero.
	  * overhead
	  * cyclic references
	  pro doesnt stop the world
  * Advantage: Work is distributed incrementally with program execution, making it suitable for real-time systems.
  * Disadvantage: Fails to reclaim cyclical data structures (e.g., a doubly-linked list where nodes point to each other) and has high overhead due to frequent counter updates.
2. Mark-Sweep:
  * How it works: Operates in two phases. First, it traverses all reachable objects from the root set and "marks" them as live. Second, it "sweeps" through the entire heap, reclaiming all unmarked objects.
  * Advantage: Correctly handles cyclical data structures.
  * Disadvantage: Can cause significant "stop-the-world" pauses and leads to heap fragmentation, where free memory is scattered in small, non-contiguous blocks.
3. Mark-Compact:
  * How it works: Identical to Mark-Sweep, but adds a third phase. After marking, it slides all live objects together to one end of the heap, eliminating fragmentation.
  * Advantage: Solves the fragmentation problem and improves data locality.
  * Disadvantage: The cost is higher than Mark-Sweep due to the multiple passes required to compute new locations and move the objects.
4. Copy Collection:
  * How it works: The heap is divided into two semi-spaces. The program allocates in one ("from-space"). During collection, all live objects are copied to the other ("to-space"). The roles of the spaces are then flipped.
  * Advantage: Allocation is extremely fast (just incrementing a pointer), and fragmentation is completely eliminated.
  * Disadvantage: It requires double the memory, as half of the heap is always idle.

10.1(u) Incremental vs. "Stop-the-World" Garbage Collection

* "Stop-the-World" GC: This approach suspends all application threads (the "mutator") while the collection cycle runs. For collectors like Mark-Sweep, this can lead to long, noticeable pauses, especially with large heaps.
* Incremental GC: This approach interleaves the work of the garbage collector with the execution of the application. It performs collection in small, discrete steps, significantly reducing the maximum pause time.

Incremental garbage collectors are essential for interactive or real-time applications where long, unpredictable pauses are unacceptable and would negatively impact user experience or system correctness.

# Writing Assignment questions
a. As compared to the heap allocation strategy, what is one advantage and one disadvantage of using the stack allocation strategy for allocating activation records?

Advantage:
Fast and automatic allocation/deallocation

Disadvantage:
Cannot handle variables whose lifetime does not follow LIFO rules. Stack frames disappear when a function returns, so stack allocation cannot support. Stack allocation is inflexible for data that must outlive its function call

b. What is meant by the term dangling reference? Provide an example program, written in C, that has a dangling reference.

A dangling reference occurs when a program holds a pointer (or reference) to a memory location after that memory has been deallocated.

```
int *p = malloc(sizeof(int));
free(p);

```


# Question 11
How is backpatching used in the csem assignment?

Pseudocode
```

```

Implementation of dowhile and 
slide 35