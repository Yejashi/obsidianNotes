### Datasets
The authors used synthetic datasets (auto-generated graphs) for controlled experiments.
This allows them to control:
- Graph Size
- Noise Level
- Query vs Data graph differences

#### Dataset 1 -> Fixed query graph
- The same query graph `Q` is used across all samples.
- Each data graph `G` is generated randomly, and the query graph `Q` is embedded into it.
- Noise is added to features → Gaussian noise (mean = 0, variance = 0.25).

Why?
- Tests ability of Sub-GMN to find the same pattern in different noisy graphs.
--> 200 training / 200 validation / 200 test samples

#### Dataset 2 -> Variable query graph
- A new random query graph is generated for each sample.
- Embedded into a random data graph.