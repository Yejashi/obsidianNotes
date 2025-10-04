![[Pasted image 20251004123121.png]]

### Driver
A common misunderstanding is that clang, the executable, is the compiler frontend. While clang does use Clang's frontend components, the executable itself is actually a kind of program called a compiler driver, or driver for short.

Compiling source code is a complex process. First, it consists of multiple phases, including the following:
- Frontend: Parsing and semantic checking
- Middle-end: Program analysis and optimization
- Backend: Native code generation
- Assembling: Running the assemble
- Linking: Running the linker

A good way to observe the hard work of a driver is to use the -### command-line flag on a normal clang invocation.

For example, you could try to compile a simple hello world program with that flag:
```
$ clang++ -### -std=c++11 -Wall ./hello_world.cpp -o
hello_world
```

The following is part of the output after running the preceding command:
```

```