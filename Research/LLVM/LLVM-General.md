### What is LLVM?
LLVM (Low Level Virtual Machine) is in essence a compiler infrastructure filled with a collection of toolchains that can be used to :
- Build new computer languages
- Improve existing language
- Develop a frontend for any programming language
- Develop a backend for any instruction set architecture

### LLVM: Intermediate Representation (IR)
LLVM's Intermediate Representation is a platform-independent, low-level programming language. It serves as the "common ground" between source code and machine code.

**Characteristics:**
- LLVM's Intermediate Representation is a platform-independent, low-level programming language. It serves as the "common ground" between source code and machine code.
- Has a typed system and three representations: 
	- textual IR, 
	- binary bitcode, 
	- in-memory IR.

Example IR Code:
```llvm
define i32 @add(i32 %a, i32 %b) {
entry:
  %sum = add i32 %a, %b
  ret i32 %sum
}
```

