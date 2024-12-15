This consists of notes i have taken on the [2016 LLVM Developers’ Meeting: A. Nemet “Compiler-assisted Performance Analysis"](https://www.youtube.com/watch?v=qq0q1hfzidg) talk.

Optimization diagnostics tell you which optimization happened, which didn't, and why not.

### Optimization Diagnostics in LLVM

Supported in LLVM and currently only a small number of passes emit them (as of 2016).

You can activate them through the `-Rpass` flag and they output in the compiler output as follows:
![[Pasted image 20241215112610.png]]

For large programs, the output of `-Rpass` is too noisy and unstructured. On top of that, messages don't appear in any particular order.

### How can this information become accessible and actionable?

The first consideration is to build on top of the existing optimization remarks (`-RPass` infrastructure)  
