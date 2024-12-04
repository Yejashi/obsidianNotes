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
- Symbol Table
	- The symbol table maps global identifiers to their corresponding LLVM entities, like functions or global variables.
- Context
	-  A module is associated with an LLVM context, which ensures thread safety and resource management. Multiple modules can share the same context.
- Linkage Unit
	-  Modules are used during the linking phase, allowing code from multiple LLVM modules to be combined into one.

LLVM API:
- In the LLVM API a module is represented by the `llvm::module` class.
- Functions in the module can be accessed using the `getFunction()` method.
- You can iterate over all functions, global variables, or metadata.

Uses:
- Modules are critical for writing LLVM passes.
- When generating LLVM IR programmatically, a module is the starting point.
- Multiple modules can be combined for link-time optimizations (LTO).

Example of an LLVM IR module in textual representation:
```llvm
; ModuleID = 'example_module' 
source_filename = "example.c" 
target triple = "x86_64-pc-linux-gnu" 

@global_var = global i32 42 

declare void @external_function()

define i32 @main() { 
entry: 
	%retval = alloca i32, align 4 
	store i32 0, i32* %retval, align 4 
	ret i32 0 
}
```

##### Functions
Functions in a module consist of:
- Header: Function signature, including name, return type, and argument list.
- Body: A series of basic blocks.

Functions in LLVM IR can be defined (`define`) or declared (`declare`).

Example:
```llvm
declare void @printf(i8* %format) ; function declaration 

define i32 @add(i32 %a, i32 %b) { ; function definition 
entry: 
	%result = add i32 %a, %b 
	ret i32 %result 
}
```


##### Basic Block
A basic block is a sequence of instructions with:
- A single entry point.
- A single exit point (usually a branch or return instruction).

Basic blocks are identified by labels.

Example:
```llvm
define void @example() {
entry:
  %x = alloca i32
  store i32 42, i32* %x
  br label %next

next:
  ret void
}
```


#### Instructions in LLVM IR
LLVM IR instructions are similar to assembly language but operate on a higher abstraction level. 

Key points:
- Strongly typed: Every variable has a type.
- SSA (Static Single Assignment) form: Each variable is assigned exactly once.
- Rich instruction set: Covers arithmetic, memory operations, control flow, and more.

##### Categories of instructions
Arithmetic
```
%sum = add i32 %a, %b
%diff = sub i32 %a, %b
```

Memory
```
%ptr = alloca i32          ; allocate memory
store i32 42, i32* %ptr    ; store value in memory
%val = load i32, i32* %ptr ; load value from memory
```

Control Flow
```
br label %next         ; unconditional branch
br i1 %cond, label %true, label %false  ; conditional branch
ret i32 0              ; return instruction
```

Function Calls
```
call i32 @add(i32 1, i32 2)
```

```
%cast = zext i8 %val to i32  ; zero-extend i8 to i32
```