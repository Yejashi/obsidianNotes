In C++, the extern keyword is used to specify linkage and indicate that a variable or function has external linkage.

This means the entity is declared, but its definition exists elsewhere, possibly in another translation unit (i.e., source file).

### The Basics of `extern`
- **Declaration vs. Definition**:
    - A declaration tells the compiler that something exists (e.g., a variable or function).
    - A definition provides the actual storage or implementation.
- **`extern` Declaration**:
    - Tells the compiler that the variable or function exists somewhere, and its definition will be resolved during linking.

### Where to use `extern`?
- Global variable
	-  If you want to share a global variable across multiple files, you declare it in a header file with `extern`, and define it in one source file.
- Functions
	- In most cases, functions are treated as having external linkage by default, so you don't usually need `extern`.
- With `extern "C"` for C-Linkage
	- C++ uses **name mangling** to support function overloading. If you need to interoperate with C code (which does not support name mangling), you use `extern "C"` to tell the compiler to avoid mangling the names.
	- 