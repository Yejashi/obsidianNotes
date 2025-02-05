- **Graph density** is a measure of how connected a graph is, relative to the total possible number of edges it could have. It describes the ratio of the number of actual edges in the graph to the number of possible edges in a complete graph (where every pair of nodes is connected).
	- Formula:
		- Undirected Graph
			- ![[Pasted image 20250126185333.png]]
		- Directed Graph
			- ![[Pasted image 20250126185354.png]]]
		- E: Number of Edges
		- N: Number of nodes
		- N(N - 1): Total number of possible edges

- A **Component** of of an undirected graph is defined as a connected subgraph that is not part of any larger connected subgraph.

- A **Connected Graph** is type of graph in which there is a path between every pair of vertices. This means that no vertex is isolated, and all vertices are reachable from any other vertex.

- **Edge connectivity** refers to the minimum number of edges that must be **removed** from a connected graph to disconnect it. 

- The **Minimum Cut** in a graph is the smallest set of edges whose removal disconnects the graph. The size of this minimum cut is equal to the edge connectivity of the graph.

- A **K-Vertex Connected Graph** is 