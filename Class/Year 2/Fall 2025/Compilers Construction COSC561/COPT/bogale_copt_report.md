Name: Befikir T. Bogale
CLASS: COSC561



### My Optimizations

**matrix_initialize_opt**
In `matrix_initialize_opt`, I moved the computation of `i * n` outside of the inner loop. This removes a repeated multiplication that does not change across iterations of the inner loop.

**array_initialization_opt**
In `array_initialize_opt`, I moved the computation of `X % Y` into a variable called `mod`, and then moved `(X % Y) * Z` into another variable called `modz`. This allowed the loop body to reduce its work to just computing `i * modz`, which eliminates redundant computations from the loop.


In `factorial_opt`, I replaced the recursive  implementation with an iterative loop. This avoids repeated function calls and reduces stack usage, making the function faster.

In `matrix_multiply_opt`, I changed the loop order from `(i, j, k)` to `(i, k, j)` and stored `A[i*n + k]` into a temporary variable before the innermost loop. This  reuses values more efficiently, leading to significantly faster matrix multiplication.
