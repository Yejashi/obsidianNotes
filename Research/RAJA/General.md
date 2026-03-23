## Elements of Loop Execution

There are three ways to launch a kernel in RAJA:
- `RAJA::forall`
	- Execute simple, non-nested loops
- `RAJA::kernel` 
	- Support nested loops and other complex loop kernels and transformations
- `RAJA::launch` 
	- Creates an execution space in which kernels are written in terms of nested loops using the `RAJA::loop` method

#### Simple Loops (`RAJA::forall`)
Consider the following loop adding two vectors:
```
for (int i = 0; i < N; ++i) {
  c[i] = a[i] + b[i];
}
```

This can be written using `RAJA::forall` as:
```
RAJA::forall<exec_policy>(RAJA::TypesRangeSegment<int>(0, N), [=] (int i) {
  c[i] = a[i] + b[i];
});
```


