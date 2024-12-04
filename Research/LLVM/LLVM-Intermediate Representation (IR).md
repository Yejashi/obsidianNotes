LLVM IR is a low-level, typed, RISC-like language designed for compilers, which balances abstraction and control. 

Its primary role is to act as a bridge between high-level language constructs and low-level machine instructions.

### Structure of an LLVM IR

#### Modules
In LLVM Intermediate Representation (LLVM IR), a module is the top-level container for all the code and data for a program or a translation unit. It is a representation of the entire program's intermediate code structure and acts as a unit of compilation.

Key Features:
- Global Scope: A module contains everything in the global scope, such as:
	- Global Variables
	- Function declarations and definitions
	- Metadata