This consists of notes i have taken on the [2016 LLVM Developers’ Meeting: A. Nemet “Compiler-assisted Performance Analysis"](https://www.youtube.com/watch?v=qq0q1hfzidg) talk.

Optimization diagnostics tell you which optimization happened, which didn't, and why not.

### Optimization Diagnostics in LLVM

Supported in LLVM and currently only a small number of passes emit them (as of 2016).

You can activate them through the `-Rpass` flag and they output in the compiler output as follows:
