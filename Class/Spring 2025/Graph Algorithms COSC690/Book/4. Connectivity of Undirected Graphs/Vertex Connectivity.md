#### Vertex Connectivity
The vertex connectivity of a graph G is the **minimum number of vertices we can delete to disconnect G or make it trivial**.

i.e For complete graphs, it is n - 1 to make it trivial.

Suppose we had the following graph:
![[Pasted image 20250205122253.png]]

If we delete verticies v
![[Pasted image 20250205125403.png]]
#### K-Vertex Connected
In graph theory, a k-vertex-connected graph is a connected graph that remains connected even after the removal of any set of fewer than k vertices. 

**Formal Definition:**
A connected graph G is said to be **k-vertex-connected** if, for every pair of vertices u and v in G, there are at least k vertex-disjoint paths connecting u and v. This means that there are at least k paths between any two vertices, and no single vertex is shared by all these paths.

In simple terms, a **k-vertex-connected graph** is a connected network where, between any two points (vertices), there are at least **k** separate paths that don't share any common points (vertices) other than the starting and ending points. This means that even if up to **k-1** points are removed, the network will still remain connected.




