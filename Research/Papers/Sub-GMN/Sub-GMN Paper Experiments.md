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

Why?
- Tests Sub-GMN’s generalization ability → can it handle unseen query graphs at test time?
-> 8000 training / 1000 validation / 1000 test samples

### Baseline Methods
To show Sub-GMN is better, they compare against two older GNN-based subgraph matching models:
- GNN: Binary classification → does node belong to subgraph (yes/no).
- FGNN: Same → binary → also does not output node-to-node mapping.

Limitation of these baselines
- They do NOT produce node-to-node mappings and only work with fixed query graphs (same as during training).
-> Sub-GMN → produces full node-to-node mapping and works with any query graph → much more flexible.

### Parameter Settings
Model hyperparameters:
- GCN → 3 layers → each outputs 128 dimensional embeddings
- Activation functions → ELU (first 2 layers), Softmax (last layer)
- NTN → k=16 (16 similarity dimensions per node pair)
- Optimizer → Adam, learning rate = 0.001
- Batch size → 128
- Training iterations → 5000 → best model selected by validation loss

### Evaluation Metrics
To compare performance:
- Accuracy: Classification → whether a data graph node is part of query graph.
- F1-Score: How precise and complete the node-to-node matching is.
- Running time: How fast the model runs → important for scalability.


