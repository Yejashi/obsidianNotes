Name: Befikir T. Bogale
CLASS: COSC561



### My Optimizations

In matrix_initialize_opt, I moved the computation of i * n outside of the inner loop. This removes a repeated multiplication that does not change across iterations of the inner loop.
