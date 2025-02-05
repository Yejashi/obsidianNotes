In graph theory, **vertex connectivity** refers to the minimum number of vertices that must be removed from a connected graph to disconnect it. 

This concept is essential for assessing the resilience of networks, as it indicates how many vertices can be removed before the network becomes disconnected.

**Formal Definition:**
Given a connected graph G=(V,E), the **vertex connectivity** κ(G) is defined as the smallest number of vertices whose removal results in a disconnected graph. In other words, it's the size of the smallest vertex cut that separates the graph into two or more disconnected components.

**Example:**
Consider a simple triangle graph with three vertices connected by three edges. Removing any single vertex from this graph will disconnect it. Therefore, the vertex connectivity of this triangle graph is 1.