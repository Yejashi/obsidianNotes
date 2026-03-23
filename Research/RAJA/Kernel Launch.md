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
- For example, if an OpenMP or CUDA parallel execution policy is used on the outermost loop, then all inner loops would be run sequentially in each thread.

The `RAJA::kernel` interface facilitates parallel execution and compile-time transformation of arbitrary loop nests and other complex loop structures. It can treat a complex loop structure as a single entity, which enables the ability to transform and apply different parallel execution patterns by changing the execution policy type and **not the kernel code**, in many cases.

The loop nest above can be written using `RAJA::kernel` as:
```
using KERNEL_POL =
  RAJA::KernelPolicy< RAJA::statement::For<N, exec_policyN,
                        ...
                          RAJA::statement::For<0, exec_policy0,
                            RAJA::statement::Lambda<0>
                          >
                        ...
                      >
                    >;

RAJA::kernel< KERNEL_POL >(
  RAJA::make_tuple(RAJA::TypedRangeSegment<int>(0, NN),
                   ...,
                   RAJA::TypedRangeSegment<int>(0, N0),

  [=] (int iN, ... , int i0) {
     // inner loop body
  }

);
```
 
In the case here, the execution policy contains a nested sequence of `RAJA::statement::For` types, indicating an iteration over each level in the loop nest.

Each of  these statement types takes three template parameters:
- An integral index parameter that binds the statement to the item in the iteration space tuple corresponding to that index
- An execution policy type for the associated loop nest level
- An _enclosed statement list_

Here, the innermost type in the kernel policy is a `RAJA::statement::Lambda<0>` type indicating that the first lambda expression (argument zero of a sequence of lambdas passed to the `RAJA::kernel` method) will comprise the inner loop body.

#### Hierarchical loops (`RAJA::launch`)
The `RAJA::launch` template is an alternative interface to `RAJA::kernel` that may be preferred for certain types of complex kernels or based on coding style preferences.

`RAJA::launch` optionally allows either host or device execution to be chosen at run time. The method takes an execution policy type that will define the execution environment inside a lambda expression for a kernel to be run on a host, device, or either. 

The `RAJA::launch` framework aims to unify thread/block based programming models such as CUDA/HIP/SYCL while maintaining portability on host back-ends (OpenMP, sequential).


