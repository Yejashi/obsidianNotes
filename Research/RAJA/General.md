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

`RAJA::forall` is a template that takes an ***execution policy*** type template parameter.

`RAJA::forall` takes two arguments:
- An iteration space object
- A single lambda expression representing the loop kernel body

#### Complex Loops (`RAJA::kernel)

The `RAJA::kernel` interface employs similar concepts to `RAJA::forall` but extends it to support much more complex kernel structures.

Each `RAJA::kernel` method is a template that takes an _execution policy_ type template parameter.
- The execution policy can be an arbitrarily complex sequence of nested templates that define a kernel execution pattern.

In its simplest form, `RAJA::kernel` takes two arguments: 
- A _tuple_ of iteration space objects
- A lambda expression representing the kernel inner loop body.

Consider the following (N + 1)-level loop nest:
```
or (int iN = 0; iN < NN; ++iN) {
  ...
     for (int i0 = 0; i0 < N0; ++i0) {s
       \\ inner loop body
     }
}
```

It is important to note that we do not recommend writing a RAJA version of this by nesting `RAJA::forall` statements. For example:
```
RAJA::forall<exec_policyN>(IN, [=] (int iN) {
  ...
     RAJA::forall<exec_policy0>(I0, [=] (int i0)) {
       \\ inner loop body
     }
  ...
}
```
This would work for some execution policy choices, but not in general. Also, this approach treats each loop level as an independent entity, which makes it difficult to parallelize the levels in the loop nest together.
- 


