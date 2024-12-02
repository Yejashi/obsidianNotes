### Phases of a program
We write programs in high-level language, which is easier for us to understand and remember. These programs are then fed into a series of tools and OS components to get the desired code that can be used by the machine. This is known as Language Processing System.

![[Pasted image 20241202074257.png]]

The high-level language is converted into binary language in various phases.

##### Preprocessor
A preprocessor, generally considered as a part of compiler, is a tool that produces input for compilers. It prepares the source code for the compiler by performing text substitution and other preprocessing tasks.

**Key Responsibilities**:
- **Header Inclusion:** Replaces `#include` directives with the actual content of the header files.
- **Macro Expansion:** Substitutes macros defined with `#define` or other preprocessor directives.
- **Conditional Compilation:** Processes `#ifdef`, `#ifndef`, `#else`, and `#endif` to include or exclude parts of the code based on conditions.
- **Other Directives:** Handles pragmas (`#pragma`), line number mappings (`#line`), and more.

**Output:** The preprocessor generates a pure C or C++ file with all the preprocessing done, typically ending in `.i` (C) or `.ii` (C++).
##### Compiler 
The **compiler** translates the preprocessed source code into assembly language, a lower-level language closer to machine code.

**Key Responsibilities:**
- **Lexical Analysis:** Breaks the source code into tokens (smallest elements like keywords, variables, and operators).
- **Syntax Analysis:** Checks if the tokens form valid statements based on grammar rules.
- **Semantic Analysis:** Ensures the statements make logical sense (e.g., type checking).
- **Intermediate Code Generation:** Creates an intermediate representation (IR), such as LLVM IR, for optimization and portability.
- **Optimization:** Improves the IR by eliminating redundancies, reorganizing instructions, etc.
- **Assembly Code Generation:** Converts the optimized IR into assembly language.

##### Assembler
An assembler translates assembly language programs into machine code.The output of an assembler is called an object file, which contains a combination of machine instructions as well as the data required to place these instructions in memory.

_TODO: Expand Later_
##### Linker
Linker is a computer program that links and merges various object files together in order to make an executable file. All these files might have been compiled by separate assemblers. The major task of a linker is to search and locate referenced module/routines in a program and to determine the memory location where these codes will be loaded, making the program instruction to have absolute references.

_TODO: Expand Later_

