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

#### A) Subgraph Matching and Matching Matrix
##### What is a graph?
A graph is:
```
Graph G = (V, E, F)

Where:
V → set of nodes
E → set of edges (connections between nodes)
F → feature function → assigns each node or edge a feature vector (optional metadata)
```

Example:
```
V = {A, B, C}
E = {(A, B), (B, C)}
F = {A: [1, 0], B: [0, 1], C: [0.5, 0.5]}
```


##### What is subgraph matching formally?
Given:
- Query graph --> Q
- Data graph --> G

You want to find a solution `m`:
```
m : V(Q) -> V(G)
```

Which maps nodes in Q to nodes in G, such that:
(1) Node match --> node features match
```
∀u ∈ V(Q): F(u) == F(m(u))
```

(2) Edge match → connected nodes are also connected in data graph
```
∀ (ua, ub) ∈ E(Q):
    → (m(ua), m(ub)) ∈ E(G)
    → AND their edge features match
```
This means → if Q has edge between A and B, their matched nodes in G must also be connected.

##### Matching Matrix *
When you find a valid mapping 'm', you can write it down as a Matching Matrix M
```
M → Shape (n, m)
n → # nodes in query graph Q
m → # nodes in data graph G

M[i][j] → 1 if query node i maps to data node j
          0 otherwise
```

Example:

| G: X | G: Y | G: Z |     |
| ---- | ---- | ---- | --- |
| Q: A | 0    | 1    | 0   |
| Q: B | 0    | 0    | 1   |

