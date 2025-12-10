Name: Befikir T. Bogale
CLASS: COSC561



### My Optimizations

**matrix_initialize_opt**
In `matrix_initialize_opt`, I moved the computation of `i * n` outside of the inner loop. This removes a repeated multiplication that does not change across iterations of the inner loop.

**array_initialization_opt**
In `array_initialize_opt`, I moved the computation of `X % Y` into a variable called `mod`, and then moved `(X % Y) * Z` into another variable called `modz`. This allowed the loop body to reduce its work to just computing `i * modz`, which eliminates constant computations from the loop.

