
Sources:
- https://dwarfstd.org/

### What is DWARF?
DWARF is a debugging information file format used by many compilers and debuggers to support source level debugging. It addresses the requirements of a number of procedural languages, such as C, C++, and Fortran, and is designed to be extensible to other languages. DWARF is architecture independent and applicable to any processor or operating system. It is widely used on Unix, Linux and other operating systems, as well as in stand-alone environments.

### How does DWARF get into the binary?
- **Compile** (`clang++ -g ...`): the frontend and backend emit DWARF records alongside machine code.
- **Assemble/Link**: the assembler puts records into `.debug_*` sections; the linker merges/relocs them.
- **(Optional) Split debug**: build keeps small binaries and writes big debug data to a side file (`.dwo`, `.debug`), referenced via `.gnu_debuglink`/build-id.
- **Use**: debuggers (or your tool via LLVM) parse these sections to reconstruct source views, call stacks, variables, etc.

### 