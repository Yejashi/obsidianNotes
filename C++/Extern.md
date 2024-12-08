In C++, the extern keyword is used to specify linkage and indicate that a variable or function has external linkage.

This means the entity is declared, but its definition exists elsewhere, possibly in another translation unit (i.e., source file).

### The Basics of `extern`
- **Declaration vs. Definition**:
    - A declaration tells the compiler that something exists (e.g., a variable or function).
    - A definition provides the actual storage or implementation.
- **`extern` Declaration**:
    - Tells the compiler that the variable or function exists somewhere, and its definition will be resolved during linking.
