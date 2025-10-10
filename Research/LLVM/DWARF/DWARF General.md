
Sources:
- https://dwarfstd.org/
- https://dwarfstd.org/doc/DWARF5.pdf

### What is DWARF?
DWARF is a debugging information file format used by many compilers and debuggers to support source level debugging. It addresses the requirements of a number of procedural languages, such as C, C++, and Fortran, and is designed to be extensible to other languages. DWARF is architecture independent and applicable to any processor or operating system. It is widely used on Unix, Linux and other operating systems, as well as in stand-alone environments.

### How Does DWARF Get Into the Binary?
- **Compile** (`clang++ -g ...`): the frontend and backend emit DWARF records alongside machine code.
- **Assemble/Link**: the assembler puts records into `.debug_*` sections; the linker merges/relocs them.
- **(Optional) Split debug**: build keeps small binaries and writes big debug data to a side file (`.dwo`, `.debug`), referenced via `.gnu_debuglink`/build-id.
- **Use**: debuggers (or your tool via LLVM) parse these sections to reconstruct source views, call stacks, variables, etc.

### Where DWARF Lives
DWARF isn’t a separate file (usually). It lives inside the binary’s **debug sections**.

When you compile with `-g`, the compiler adds extra sections into your ELF:
```
.text              → machine code
.data              → global/static data
.debug_info        → descriptions of functions, variables, etc.
.debug_abbrev      → “schema” telling how DIEs are structured
.debug_line        → mapping of addresses ↔ source lines
.debug_str         → strings used by DWARF entries
.debug_ranges      → list of discontiguous address ranges
```
### Core Data Model
DWARF represents the program as a **tree of “DIEs” (Debugging Information Entries)**.

For example:
```
Compile Unit (foo.cpp)
├── subprogram "main"       (DW_TAG_subprogram)
│     ├── variable "argc"   (DW_TAG_variable)
│     ├── variable "argv"   (DW_TAG_variable)
│     └── lexical_block
│          └── call "bar"
└── subprogram "bar"        (DW_TAG_subprogram)
```

Every node has:
- a **tag** (e.g., `DW_TAG_subprogram`, `DW_TAG_variable`)
- a list of **attributes** (e.g., `DW_AT_name`, `DW_AT_low_pc`, `DW_AT_high_pc`, `DW_AT_decl_line`)

#### A Simple Example
Consider the following application:
```
int bar() { return 42; }

int main() {
  int x = bar();
  return x;
}
```

DWARF will record:
- A **compile unit** for `main.cpp`
- Inside it:
    - A DIE for `main()` (a `DW_TAG_subprogram`)
    - A DIE for `bar()` (another `DW_TAG_subprogram`)
- Each function DIE will have:
    - `DW_AT_name = "main"`
    - `DW_AT_low_pc = 0x401000`
    - `DW_AT_high_pc = 0x401045`
    - `DW_AT_decl_file = 1` (index into a file table)
    - `DW_AT_decl_line = 3`

You can look at a machine address (e.g., `0x401010`) and ask:  
- “Which DIE’s PC range covers this?” → “main()” → line 3 in `main.cpp`.


#### The Line Table
There is a table in the `.debug_line` section that contains translations of PC addressess to file and line numbers.

| Address  | File     | Line |
| -------- | -------- | ---- |
| 0x401000 | main.cpp | 3    |
| 0x401005 | main.cpp | 4    |
| 0x401010 | main.cpp | 5    |
| 0x401015 | main.cpp | 6    |
This is how stack traces show:
```
#0  bar() at main.cpp:2
#1  main() at main.cpp:5
```


