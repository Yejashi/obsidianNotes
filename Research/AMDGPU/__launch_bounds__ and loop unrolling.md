`__launch_bounds__` tells the compiler what block size you _promise_ to use when launching the kernel, so it can make better register and unrolling decisions.

It does **not** change how many threads actually run.  
It **changes how aggressively the compiler uses registers and unrolls code**.

This does **not** mean:
- The compiler changes how many threads are launched at runtime 
- The compiler magically knows the launch configuration

It does mean:
- The compiler is being given constraints about the launch configuration so it can make safer backend decisions, especially about registers, unrolling, and spilling.

The semantics of `__launch_bounds__`
