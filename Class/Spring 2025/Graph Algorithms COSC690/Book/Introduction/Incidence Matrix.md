An **incidence matrix** is another way to represent a graph, but unlike the adjacency matrix, it relates the graph's vertices to its edges. In this representation, the rows of the matrix correspond to the vertices, and the columns correspond to the edges.

### Key Characteristics of an Incidence Matrix:
1. **Vertices**: Each row of the matrix represents a vertex in the graph.
2. **Edges**: Each column represents an edge in the graph.
3. **Entries**: The entries in the incidence matrix indicate the relationship between vertices and edges. Specifically:
    - For an **undirected graph**, the matrix entry is **1** if the vertex is incident (connected) to the edge, and **0** if it is not.
    - For a **directed graph**, the matrix entry is **-1** if the vertex is the tail (source) of the edge, **1** if the vertex is the head (destination) of the edge, and **0** if the vertex is not connected to the edge.

![[Pasted image 20250126162340.png]]

