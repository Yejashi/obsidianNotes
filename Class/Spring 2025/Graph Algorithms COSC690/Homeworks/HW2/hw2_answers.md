
#### 1. Let λ(G) denote the edge-connectivity of a graph G. Show that if λ(G) = k ≥ 2, then the deletion of k edges from G results in a graph with at most 2 components. Is there a similar result for vertex-connectivity?

Suppose we had the following graph:

![[Pasted image 20250205133330.png]]

Which has an edge connectivity of 2, as shown:
![[Pasted image 20250205133356.png]]

We can see that with a graph like this, the minimum degree for any node is now 2. As such, regardless of how the graph changes, if the minimum degree is less than 2 then it cannot have an edge connectivity of λ(G) = k ≥ 2.

We will also have a similar result for vertex connectivity.

For example, the same graph as above has a vertex connectivity of 2:
![[Pasted image 20250205134018.png]]

If the original were to have so much as an additional edge for any vertex, making the degree of said vertex greater than 2, then it would immediately have a vertex connectivity of 1, which is not λ(G) = k ≥ 2.


#### 2. Topological sort orders the vertices of a directed graph such that for every directed edge (u, v) from vertex u to vertex v, u comes before v in the ordering. Given the following graph, state the linear ordering of vertices by performing a topological sort using the conditions below. In every case where a choice needs to be made, choose the smallest vertex label

![[Pasted image 20250205134615.png]]

##### **a.)** Using DFS
![[Pasted image 20250205141700.png]]

##### b.) Using BFS
![[Pasted image 20250205142558.png]]


#### c.) Which method has a better time complexity? Why?



#### 3. Consider the following recursive algorithm. It takes as input a simple, undirected graph G and returns an output of True/False if the graph is connected.
![[Pasted image 20250205140626.png]]
##### a. Does this algorithm work correctly for every simple, undirected graph of size n > 0?

This algorithm will fail if there is a graph with two components because it only checks if at least one, which is not adequate.

Example:
![[Pasted image 20250205143539.png]]

##### b. On which graphs does this algorithm reach the final return statement?

The algorithm will reach the final return statement if there is a graph with node of degree 0.

##### c. On what type(s) of graph(s) does the worst-case behavior occur? What about the best?

The worst case behavior occurs when there is a graph such that all the edges connect to a single. This will cause a setting where a full column in the adjacency matrix is are all 1's and the rest of the columns are 

