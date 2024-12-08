#### Pass Manager Issue
The default clang compiler on Dane is `clang/14.0.6` with LLVM 14. This is an issue because it means i can't use the new pass manager and am restricted to the legacy pass manager.

#### Potential Bug?

```
(base) [bogale2@dane3:build]$ opt -load-pass-plugin ./lib/HelloWorldPass.so -passes="hello-world" -disable-output test_1.ll
opt: CommandLine Error: Option 'debug-pass' registered more than once!
LLVM ERROR: inconsistency in registered CommandLine options
PLEASE submit a bug report to https://github.com/llvm/llvm-project/issues/ and include the crash backtrace.
Stack dump:
```

For some reason, i can't run the passes without having the `-debug-pass` flag causing issues.

Setup:
- System: Dane
- Clang: `clang/14.0.6`

Potential Fixes:
- [`-DENABLE_LLVM_SHARED=1`](https://github.com/bpftrace/bpftrace/issues/1855)
	- This does not seem to work.