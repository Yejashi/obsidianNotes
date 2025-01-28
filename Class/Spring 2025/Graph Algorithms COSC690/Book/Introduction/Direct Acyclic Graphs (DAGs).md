A **Directed Acyclic Graph (DAG)** is a type of directed graph that has two key properties:
- **Directed**: The edges of the graph have a direction, meaning each edge points from one vertex to another (just like in a directed graph).
- **Acyclic**: The graph does not contain any cycles, meaning there is no way to start at a vertex and follow a path of directed edges that eventually leads back to the same vertex.

A directed graph is a DAG if and only if it can be topologically ordered, by arranging the vertices as a linear ordering that is consistent with all edge directions.

A topological ordering of a directed graph is an ordering of its vertices into a sequence, such that for every edge the start vertex of the edge occurs earlier in the sequence than the ending vertex of the edge.

