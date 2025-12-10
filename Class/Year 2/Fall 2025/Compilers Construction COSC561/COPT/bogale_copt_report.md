Name: Befikir T. Bogale
CLASS: COSC561



### My Optimizations

**matrix_initialize_opt**
In `matrix_initialize_opt`, I moved the computation of `i * n` outside of the inner loop. This removes a repeated multiplication that does not change across iterations of the inner loop.

**array_initialization_opt**
In `array_initialize_opt`, I moved the computation of `X % Y` into a variable called `mod`, and then moved `(X % Y) * Z` into another variable called `modz`. This allowed the loop body to reduce its work to just computing `i * modz`, which eliminates redundant computations from the loop.

**factorial_opt**
In `factorial_opt`, I replaced the recursive  implementation with an iterative loop. This avoids repeated function calls and reduces stack usage, making the function faster.

**matrix_multiply_opt**
In `matrix_multiply_opt`, I changed the loop order from `(i, j, k)` to `(i, k, j)` and stored `A[i*n + k]` into a temporary variable before the innermost loop. This  reuses values more efficiently, leading to faster matrix multiplication.


### Performance Results

**Reference Implementation**
```
(base) bbogale:hydra12 ~/CLASS/Fall2025/CompilersConstruction/copt> ./test.sh copt_O3_ref   <-  2:38PM
Running MATRIX_INIT with n = 3000 loop = 200

UNOPTIMIZED(ms):        1566.0
OPTIMIZED(ms):          1767.0
SPEEDUP:                  0.89

Running ARRAY_INIT with n = 300000 loop = 20000

UNOPTIMIZED(ms):         950.0
OPTIMIZED(ms):          1716.0
SPEEDUP:                  0.55

Running FACTORIAL with n = 20 loop = 200000000

UNOPTIMIZED(ms):        1966.0
OPTIMIZED(ms):          1917.0
SPEEDUP:                  1.03

Running MATRIX_MULTIPLY with n = 1600 loop = 1

UNOPTIMIZED(ms):        7983.0
OPTIMIZED(ms):          1667.0
SPEEDUP:                  4.79
```



**My Implementation**
```
(base) bbogale:hydra12 ~/CLASS/Fall2025/CompilersConstruction/copt> ./test.sh copt_O3       <-  2:38PM
Running MATRIX_INIT with n = 3000 loop = 200

UNOPTIMIZED(ms):        1650.0
OPTIMIZED(ms):          1583.0
SPEEDUP:                   1.0

Running ARRAY_INIT with n = 300000 loop = 20000

UNOPTIMIZED(ms):         983.0
OPTIMIZED(ms):           983.0
SPEEDUP:                   1.0

Running FACTORIAL with n = 20 loop = 200000000

UNOPTIMIZED(ms):        2133.0
OPTIMIZED(ms):          2083.0
SPEEDUP:                   1.0

Running MATRIX_MULTIPLY with n = 1600 loop = 1

UNOPTIMIZED(ms):        7500.0
OPTIMIZED(ms):           966.0
SPEEDUP:                   7.8
```


### Questions
