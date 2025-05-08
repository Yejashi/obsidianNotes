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

|      | G: X | G: Y | G: Z |
| ---- | ---- | ---- | ---- |
| Q: A | 0    | 1    | 0    |
| Q: B | 0    | 0    | 1    |
Meaning:
```
Q node A → G node Y
Q node B → G node Z
```

> This is the core target of the Sub-GMN model → Predict this Matching Matrix.
> In training → Ground-truth Matching Matrix is used as supervision (model learns to predict it).
> In inference → Model outputs Matching Matrix → gives node-to-node mappings.


#### B) Graph Convolutional Networks (GCN)

##### Why Do We Need Embeddings?

If you want to compare nodes from Query Graph and Data Graph → you can’t compare raw node ids → meaningless.

You need to:
- Encode node attributes
- Encode node structure (its neighbors)
-->  into a vector representation (embedding).

##### How does GCN work?
Formula (you see this everywhere):
```
H^(l+1) = f( A_hat × H^l × W^l )
```
Where:
- `H^l` --> node embeddings at layer `l` (initially -> raw features)
- `A_hat` --> normalized adjacency matrix (how nodes are connected)
- `W^l` --> learnable weight matrix
- `f` --> activation function (ReLU, ELU, etc)

What happens:
- Aggregate neighbor embeddings → sum / mean / weighted sum.
- Apply linear transformation.
- Apply non-linear activation → produce new embedding.

Multiple layers → aggregate multi-hop neighbors.

##### Why is This Good?
- Captures local structure --> neighbors info.
- Captures node features.
- Produces embeddings of same size for all graphs --> needed to compare nodes Q and G

> In Sub-GMN → same GCN (shared weights) is used for query graph and data graph → so embeddings are comparable.

#### C) Neural Tensor Network (NTN)
Now you have:
```
Query node embedding → e1
Data graph node embedding → e2
```

How to compare them? → You need a similarity function.
Simple methods:
- Dot product → too simple
- Cosine similarity → too simple
--> They only capture simple relations.

NTN --> more powerful -->learns complex relation patters

##### What Does NTN Do?
Formula:
```
g(e1, e2) = f ( e1^T × W[1:k] × e2 + V × [e1; e2] + b )
```

Where:
- `W[1:k]` --> tensor --> k learnable matrices --> each slice compares `e1` and `e2` differently.
- `V` --> linear transformation on concatenated `e1` and `e1`.
- `b` --> bias
- `f` --> non-linearity (sigmoid, etc)

Output → k scores → similarity representation across k dimensions.

NTN can learn patterns like:
- "If feature X in query matches feature Y in data → this is important."
- "If neighbor pattern is similar → boost score."

### 3. Model

What is the purpose of Sub-GMN (in plain language)?
- Take a pair of graphs → (Query Graph Q, Data Graph G).
- For each query graph node → figure out which node(s) in the data graph it best matches.
- Output → a Matching Matrix (Query node vs Data node → probabilities).

Overview: The model has **three stages**, each carefully building toward the final matching matrix:
```
Stage 1 → Create node embeddings (GCN)
Stage 2 → Compare node pairs to compute similarity (NTN + Attention)
Stage 3 → Compress similarity → produce Matching Matrix
```

#### Stage 1 - Node Embedding (with GCN)

Formula (revisited):
```
H^(l+1) = f( A_hat × H^l × W^l )
```
Where:
- `H^l` --> node embeddings at layer `l` (initially -> raw features)
- `A_hat` --> normalized adjacency matrix (how nodes are connected)
- `W^l` --> learnable weight matrix
- `f` --> activation function (ReLU, ELU, etc)

Why shared weights between query graph and data graph?
- If `Q` and `G` both use the same GCN weights → nodes that have similar structures → produce similar embeddings → makes comparison fair.

```
Query Graph → GCN → Node embeddings → Hq
Data Graph → GCN → Node embeddings → Hg
```

This gives us → two sets of embeddings → ready for comparison.

#### Stage 2 - Similarity Tensor (NTN + Attention)

Now that we have embeddings for Query Graph and Data Graph nodes:
