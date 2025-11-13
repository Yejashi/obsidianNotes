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

![[Pasted image 20251112182055.png]]

# Question 7

Give the three-address code that could be emitted to translate the following assignment statement. However, you may not use array index operations. Assume that a is an integer array with 5 rows and 10 columns. Assume that v is an integer variable and i and j are integer parameters passed to the function. Provide solutions for when 1) the arrays are stored in row major order, and 2) the arrays are stored in column major order.

# Question 10
**(a) Why is bottom-up parsing (with one symbol of lookahead) more powerful than top-down parsing (with one lookahead symbol)?**

Bottom-up (LR) parsers can handle a **larger class of context-free grammars** than top-down (LL) parsers.
-  LL(1) parsers require grammars to be **left-factored and free of left recursion**, which limits their expressiveness.
- LR(1) parsers work **without modifying the grammar**, handling **left recursion and ambiguity resolution** automatically using a deterministic PDA. As such,  LR(1) parsing can recognize more grammars than LL(1)

**(b) Explain the different error recovery strategies.**

**Panic-mode recovery** – Keep parsing until a synchronizing token is found. (e.g. semicolon)
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
        
- **Jump table:**
    - Builds a **table of case labels** indexed by expression value.
    - **O(1)** dispatch; best for **dense, contiguous** case ranges.
    - Requires extra data space.

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
