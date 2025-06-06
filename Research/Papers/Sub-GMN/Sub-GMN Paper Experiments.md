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

#### How is Accuracy Calculated?
For each data graph:
- `NOCC` = number of correctly classified nodes (i.e., in query graph).
- `TNON` = total number of nodes in data graph.
```
acccuraacy = NOCC / TNON
```

#### How is F1-Score Calculated?
```
F1 = 2 * (Precision * Recall) / (Precision + Recall)

Precision = correct matches / all predicted matches
Recall = correct matches / all actual matches
```

F1-Score is important because it measures exact matching accuracy → this is the true test for subgraph matching.

### Results
#### Compared with GNN (Dataset 1)
|Model|Average Accuracy|
|---|---|
|GNN|~84%|
|Sub-GMN|~98%|
Sub-GMN → +12% better → also MUCH more stable (GNN accuracy varied wildly → unstable on different query sizes).

#### Compared with FGNN (Dataset 2)
|Model|Average Accuracy|
|---|---|
|FGNN|~96%|
|Sub-GMN|~99%|
Sub-GMN → +3% better → much more stable especially when query and data graphs are very different.

|Task|FGNN|Sub-GMN|
|---|---|---|
|Small graph|6ms|1ms|
|Large graph (300 nodes)|300ms|35ms|
Sub-GMN is 20–40x faster than FGNN, especially on large graphs.

#### Results on Dataset 2 (Variable Query Graph)
|Metric|Sub-GMN|
|---|---|
|Accuracy|~96.9%|
|F1-score|~0.95|
 Most important point → Sub-GMN works even when query graph is different in every sample → TRUE generalization ability.