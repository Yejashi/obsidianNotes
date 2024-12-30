Generate data for dalal that she cal use in her model. 
She wants at least 1000x1000 points.

First attempts was to try to vary `n_ranks` and `n_threads_per_proc`. Realisticly this would not generate us as many points as we would need as the hardware we're operating on is limited.

instead we'll have to look int varying problem parameters specific to the benchmarks.

WIth the OCI approach only some of the benchmarks works.