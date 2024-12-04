### Libraries
#### Static Libraries
A static library is a collection of compiled object files that are linked directly into a program at compile-time. The resulting executable contains all the code it needs from the library.

### Phases of a program translation
We write programs in high-level language, which is easier for us to understand and remember. These programs are then fed into a series of tools and OS components to get the desired code that can be used by the machine. This is known as Language Processing System.

![[Pasted image 20241202074257.png]]

The high-level language is converted into binary language in various phases.

#### Preprocessor
A preprocessor, generally considered as a part of compiler, is a tool that produces input for compilers. It prepares the source code for the compiler by performing text substitution and other preprocessing tasks.

**Key Responsibilities**:
- **Header Inclusion:** Replaces `#include` directives with the actual content of the header files.
- **Macro Expansion:** Substitutes macros defined with `#define` or other preprocessor directives.
- **Conditional Compilation:** Processes `#ifdef`, `#ifndef`, `#else`, and `#endif` to include or exclude parts of the code based on conditions.
- **Other Directives:** Handles pragmas (`#pragma`), line number mappings (`#line`), and more.

**Output:** The preprocessor generates a pure C or C++ file with all the preprocessing done, typically ending in `.i` (C) or `.ii` (C++).

You can see how it affects code by doing `gcc -E foo.c` or `clang -E foo.c`

#### Compiler 
The **compiler** translates the preprocessed source code into assembly language, a lower-level language closer to machine code.

**Key Responsibilities:**
- **Lexical Analysis:** Breaks the source code into tokens (smallest elements like keywords, variables, and operators).
- **Syntax Analysis:** Checks if the tokens form valid statements based on grammar rules.
- **Semantic Analysis:** Ensures the statements make logical sense (e.g., type checking).
- **Intermediate Code Generation:** Creates an intermediate representation (IR), such as LLVM IR, for optimization and portability.
- **Optimization:** Improves the IR by eliminating redundancies, reorganizing instructions, etc.
- **Assembly Code Generation:** Converts the optimized IR into assembly language.

**Output:** The compiler produces an assembly file (e.g., `.s`).
#### Assembler
An assembler translates assembly language programs into machine code.The output of an assembler is called an object file, which contains a combination of machine instructions as well as the data required to place these instructions in memory.

**Key Responsibilities:**

- **Translation to Machine Code:** Converts mnemonics (like `MOV`, `ADD`) into their binary equivalents.
- **Symbol Table Management:** Resolves symbolic references like labels to memory addresses.
- **Relocation Information:** Marks sections of the code/data for linking.

**Output:** The assembler creates an object file (e.g., `.o` or `.obj`), which is a binary file containing machine code and some metadata.
#### Linker
The **linker** combines one or more object files into a single executable file. It resolves cross-references between different object files and external libraries.

**Key Responsibilities:**

- **Symbol Resolution:** Links function calls and variable references to their definitions across object files or libraries.
- **Relocation:** Adjusts addresses in the code and data sections to reflect the executable's memory layout.
- **Library Linking:** Integrates code from libraries (static or dynamic) into the program.
- **Executable Generation:** Produces an executable binary file ready to be loaded into memory and run.

**Output:** The linker generates an executable file (e.g., `.exe`, `.out`, or platform-specific binaries).

***

### Different Phases of a Compiler

![[Pasted image 20241202080611.png]]

### Lexical Analysis 
The first phase of the compiler is **lexical analysis** (scanning), where the source code is analyzed character by character to break it down into meaningful units called **tokens**.

**Key Responsibilities:**
- **Tokenization:** The source code is split into tokens, which are the smallest units like keywords (`if`, `int`), identifiers (variable names), literals (`123`, `'a'`), operators (`+`, `=`), and punctuation (`;`, `{`).
- **Error Detection:** Detects invalid tokens, such as unknown symbols or malformed literals.
- **Symbol Table Creation:** Stores information about identifiers, such as their names, types, and scope.

**Output:** A sequence of tokens, often fed into the next phase. 

For example, `int a = 5;` might generate:
```c
Token: 'int', 'a', '=', '5', ';'
```

### Syntax Analysis 
The second phase is **syntax analysis**, which checks if the sequence of tokens adheres to the grammar rules of the programming language.

**Key Responsibilities:**
- **Constructing Parse Trees:** Generates a tree-like structure (parse tree) that represents the grammatical structure of the code.
- **Grammar Validation:** Ensures the code follows the syntactic rules. For example, `int a = ;` would be flagged because it's missing a value.
- **Error Reporting and Recovery:** Reports syntax errors and attempts to recover to continue parsing.

**Output:** A **parse tree** or **syntax tree**. 

For example, the tree for `int a = 5;` might look like:
```
   =
 /   \
int   5
```

### Semantic Analysis 
The **semantic analysis** phase ensures that the parsed code makes logical sense and adheres to the rules of the language.

**Key Responsibilities:**
- **Type Checking:** Ensures variables and expressions have compatible types (e.g., adding an integer to a string is invalid).
- **Scope and Declaration Checking:** Verifies that variables are declared before use and are used within their scope.
- **Semantic Error Detection:** Flags issues such as function calls with incorrect arguments or misuse of operators.

**Output:** An annotated syntax tree with semantic information, or errors if issues are found. For instance, calling a function with the wrong number of arguments might be flagged here.

### Intermediate Code Generation 
The **intermediate code generation** phase converts the semantic representation of the code into a simplified, intermediate representation (IR) that is easier to optimize and portable across platforms.

**Key Responsibilities:**
- **IR Construction:** Produces code in a platform-independent format such as three-address code, quadruples, or LLVM IR.
- **Simplification:** Abstracts machine-level details, focusing on logical operations.

**Output:** Intermediate code.

For example, the expression `a = b + c * d` might be represented as:
```c
t1 = c * d
t2 = b + t1
a = t2
```

### Code Optimization
The **code optimization** phase refines the intermediate code to make it more efficient without changing its functionality.

**Key Responsibilities:**
- **Dead Code Elimination:** Removes code that has no effect on the program (e.g., unused variables or unreachable code).
- **Loop Optimization:** Improves performance of loops (e.g., unrolling loops or reducing loop overhead).
- **Constant Folding:** Evaluates constant expressions at compile time (e.g., `3 + 4` becomes `7`).
- **Strength Reduction:** Replaces expensive operations with cheaper ones (e.g., replacing multiplication by addition).

**Output:** Optimized Intermediate code.

### Target Code Generation
The **target code generation** phase converts the optimized intermediate code into machine code specific to the target architecture (e.g., x86, ARM).

**Key Responsibilities:**
- **Instruction Selection:** Maps high-level operations to specific machine instructions.
- **Register Allocation:** Allocates CPU registers for variables and intermediate values.
- **Address Translation:** Determines the memory addresses for variables and instructions.
- **Code Emission:** Generates binary instructions for the target platform.

**Output:** The final **machine code** or executable program.   

