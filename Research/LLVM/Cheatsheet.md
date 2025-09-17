##### Generate LLVM IR (Textual)
```bash
clang -S -emit-llvm -o example.ll example.c
```

##### Run Optimizations
```bash
opt -O3 example.ll -o optimized.bc
```

##### Convert to Assemble
```bash
llc optimized.bc -o example.s
```

##### Compile to Binary
```bash
clang example.s -o example
```

**Demangle Symbol**
```
llvm-cxxfilt -n
```