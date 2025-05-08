#### Problems with Exact Subgraph Matching
- Very slow for large graphs.
- Sensitive to noise → If query graph structure does not exactly exist → returns nothing.

#### Inexact/approximate methods -> the solution
To solve the practical version of the problem, we allow "approximate" matches:
- Tolerate noise.
- Find close enough subgraphs, even if they aren't exactly isomorphic.

Prior methods (Saga, Tale, G-Finder) used **heuristics**:
- 