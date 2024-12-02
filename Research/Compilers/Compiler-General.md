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


