#### [Current limitations](https://clang.llvm.org/docs/UsersManual.html#id25)[](https://clang.llvm.org/docs/UsersManual.html#current-limitations "Link to this heading")
1. Optimization remarks that refer to function names will display the mangled name of the function. Since these remarks are emitted by the back end of the compiler, it does not know anything about the input language, nor its mangling rules.
2. Some source locations are not displayed correctly. The front end has a more detailed source location tracking than the locations included in the debug info (e.g., the front end can locate code inside macro expansions). However, the locations used by -Rpass are translated from debug annotations. That translation can be lossy, which results in some remarks having no location information.


