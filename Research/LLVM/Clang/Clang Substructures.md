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

Solving these challenges requires close cooperation between the preprocessor and the lexer, which provides primitives for all the preprocessing actions

Their source code can be found under `clang/lib/Lex`. 

#### Parser and Sema
Clang's parser consumes token streams from the preprocessor and lexer and tries to realize their semantic structures

Here, the Sema sub-system performs more semantic checking and analysis from the parser's result before generating the AST. 

#### AST
The AST is the most important primitive when it comes to extending Clang with your custom logic

All the common Clang extensions/plugins that we will introduce operate on an AST. To get a taste of AST, you can use the following command to print out the an AST from the source code:
```
$ clang -Xclang -ast-dump -fsyntax-only foo.c
```

For example, on my computer, I have used the following simple code, which only contains one function:
```
int foo(int c) { return c + 1; }
```

This will yield the following output:
```
TranslationUnitDecl 0x560f3929f5a8 <<invalid sloc>> <invalid
sloc>
|…
`-FunctionDecl 0x560f392e1350 <./test.c:2:1, col:30> col:5
foo 'int (int)'
|-ParmVarDecl 0x560f392e1280 <col:9, col:13> col:13 used c
'int'
`-CompoundStmt 0x560f392e14c8 <col:16, col:30>
`-ReturnStmt 0x560f392e14b8 <col:17, col:28>
`-BinaryOperator 0x560f392e1498 <col:24, col:28> 'int'
'+'
|-ImplicitCastExpr 0x560f392e1480 <col:24> 'int'
<LValueToRValue>
| `-DeclRefExpr 0x560f392e1440 <col:24> 'int' lvalue
ParmVar 0x560f392e1280 'c' 'int'
`-IntegerLiteral 0x560f392e1460 <col:28> 'int' 1
```

This command is pretty useful because it tells you the C++ AST class that represents certain language directives, which is crucial for writing AST callbacks – the core of many Clang plugins. 

For example, from the previous lines, we can know that a variable reference site (`c` in the `c + 1` expression) is represented by the `DeclRefExpr` class.

#### Codegen

Though there are no prescriptions for how you should process the AST (for example, if you use the `-ast-dump` command-line option shown previously, the frontend will print the textual AST representation), the most common task that's performed by the CodeGen subsystem is emitting the LLVM IR code, which will later be compiled into native assembly or object code by LLVM.

### LLVM, assemblers, and linkers
Once the LLVM IR code has been emitted by the CodeGen subsystem, it will be processed by the LLVM compilation pipeline to generate native code, either assembly code or object code.

LLVM provides a framework called the **MC layer**, in which architectures can choose to implement assemblers that have been directly integrated into LLVM's pipeline