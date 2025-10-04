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
"/path/to/clang" "-cc1" "-triple" "x86_64-apple-
macosx11.0.0" "-Wdeprecated-objc-isa-usage" "-
Werror=deprecated-objc-isa-usage" "-Werror=implicit-
function-declaration" "-emit-obj" "-mrelax-all" "-
disable-free" "-disable-llvm-verifier" … "-fno-
strict-return" "-masm-verbose" "-munwind-tables" "-
target-sdk-version=11.0" … "-resource-dir"
"/Library/Developer/CommandLineTools/usr/lib/clang/1
2.0.0" "-isysroot"
"/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk
" "-I/usr/local/include" "-stdlib=libc++" … "-Wall"
"-Wno-reorder-init-list" "-Wno-implicit-int-float-
conversion" "-Wno-c99-designator" … "-std=c++11" "-
fdeprecated-macro" "-fdebug-compilation-dir"
"/Users/Rem" "-ferror-limit" "19" "-fmessage-length"
"87" "-stack-protector" "1" "-fstack-check" "-
mdarwin-stkchk-strong-link" … "-fexceptions" … "-
fdiagnostics-show-option" "-fcolor-diagnostics" "-o"
"/path/to/temp/hello_world-dEadBeEf.o" "-x" "c++"
"hello_world.cpp"…
```

These are essentially the flags being passed to the real Clang frontend after the driver's translation.

The source code for the driver can be found under `clang/lib/Driver`.

### Frontend
A typical compiler textbook might tell you that a compiler frontend consists of a **lexer** and a **parser**, which generates an **abstract syntax tree (AST)**. Clang's frontend also uses this skeleton, but with some major differences. 

First, the **lexer** is usually coupled with the preprocessor, and the semantic analysis that's performed on the source code is detached into a separate subsystem, called the **Sema**. This builds an AST and does all kinds of semantic checking.

#### Lexer and Preprocessor
Due to the complexity of programming language standards and the scale of real- world source code, preprocessing becomes non-trivial

For example, resolving included files becomes tricky when you have 10+ layers of a header file hierarchy, which is common in large-scale projects

Advanced directives such as #pragma can be challenged in cases where OpenMP uses #pragma to parallelize for loops