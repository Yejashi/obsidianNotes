An adjacency list is a way to represent a graph, where each vertex in the graph is associated with a list (or another type of collection) that contains all the vertices that it is directly connected to by an edge. 

This representation is efficient in terms of memory usage, especially for sparse graphs (graphs with relatively few edges compared to the number of vertices).

![[Pasted image 20250126161612.png]]

### Key Characteristics of an Adjacency List:
1. **Vertices**: Each vertex in the graph has a corresponding entry in the list.
2. **Edges**: The list associated with each vertex contains all the other vertices to which it is connected. For an undirected graph, if there is an edge between vertices **A** and **B**, both **A** will list **B** as an adjacent vertex, and **B** will list **A** as an adjacent vertex. In a directed graph, the edge direction matters, so **A** lists **B** but **B** does not necessarily list **A**.
3. **Efficiency**: The adjacency list is efficient for sparse graphs because it only stores edges that exist, rather than storing every possible edge between all pairs of vertices (which would be done in an adjacency matrix).