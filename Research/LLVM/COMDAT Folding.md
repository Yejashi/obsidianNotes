COMDAT folding is a linker optimization used to deduplicate identical functions or data that appear in multiple object files, ensuring only one copy ends up in the final binary.

It commonly occurs in C++ builds where templates, inline functions, and header-defined code are compiled into many translation units.

### Why COMDAT Exists

In C/C++ builds, multiple object files may contain **identical definitions** of the same function or data. For example:
```
inline int add(int a, int b) {  
return a + b;  
}
```

If this header is included in **10 source files**, the compiler may emit **10 copies of `add()`**.

The linker must decide what to do with these duplicates.

Without COMDAT, this would cause **multiple definition errors**.

