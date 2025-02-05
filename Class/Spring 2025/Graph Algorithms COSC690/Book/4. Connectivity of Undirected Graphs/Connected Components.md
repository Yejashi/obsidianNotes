#### What is a component?
In graph theory, a **component** of an undirected graph is defined as a connected subgraph that is not part of any larger connected subgraph. This means that within a component, there exists a path between any pair of vertices, and no additional vertices from the original graph can be included without losing this property.

#### What is a connected component?
In graph theory, a **connected component** of an undirected graph is a **maximal subgraph in which any two vertices are connected to each other by paths,** and which is connected to no additional vertices in the rest of the graph. In simpler terms, it's a **subset of the graph where there's a path between any pair of vertices within that subset, and no vertex in the subset is connected to any vertex outside of it**.

**Key Characteristics:**
- **Partitioning:** The vertices of a graph are partitioned into disjoint sets by its components. Each component is an induced subgraph formed by the vertices reachable from any vertex within that component.
- **Connected Graphs:** A graph that is entirely connected consists of a single component encompassing all its vertices.
- **Disconnected Graphs:** Graphs that are not connected comprise multiple components, each being a maximal connected subgraph.

**A component of graph G is a maximal connected subgraph of G.**

**Key Points:**
- **Maximality:** A connected component is maximal, meaning that adding any more vertices to it would break its property of being connected.
- **Disjoint Subsets:** The entire graph can be partitioned into disjoint connected components. Each vertex belongs to exactly one connected component.

![[Pasted image 20250205111804.png]]

