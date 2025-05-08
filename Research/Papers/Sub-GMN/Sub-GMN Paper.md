### 1. Introduction
#### Problems with Exact Subgraph Matching
- Very slow for large graphs.
- Sensitive to noise → If query graph structure does not exactly exist → returns nothing.

#### Inexact/approximate met
hods -> the solution
To solve the practical version of the problem, we allow "approximate" matches:
- Tolerate noise.
- Find close enough subgraphs, even if they aren't exactly isomorphic.

Prior methods (Saga, Tale, G-Finder) used **heuristics**:
- Select a seed node.
- Expand neighbors using rules.
- Enumerate possible matches.

#### Limitations of prior GNN-based Subgraph Matchers
- GNN and FGNN → binary classification on nodes → yes/no only → does not give node-to-node mapping.
- Can only match query graphs seen during training.
This means → no generalization to new query graphs.

#### Sub-GMN: Proposed Solution
- Takes a pair of graphs (data, query) --> so new query graphs are supported at inference.
- Learns none-to-node similarity (matching matrix) --> not just binary classification.
- Combines:
	- GCN --> to embed nodes
	- Neural Tensor Network (NTN) --> to compute pairwise node similarity
	- Attention --> to make comparisons context-aware

Result:
- Can match any new query graph.
- Produces node-to-node mapping (matching matrix).

### 2. Preliminary


