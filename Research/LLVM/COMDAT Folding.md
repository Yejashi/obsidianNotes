COMDAT folding is a linker optimization used to deduplicate identical functions or data that appear in multiple object files, ensuring only one copy ends up in the final binary.

It commonly occurs in C++ builds where templates, inline functions, and header-defined code are compiled into many translation units.

