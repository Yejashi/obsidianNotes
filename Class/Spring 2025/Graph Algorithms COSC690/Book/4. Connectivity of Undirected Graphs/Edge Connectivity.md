In graph theory, **edge connectivity** refers to the minimum number of edges that must be removed from a connected graph to disconnect it. 

This concept is crucial for understanding the resilience of networks, as it indicates how many edges can be removed before the network becomes disconnected.

**Formal Definition:**
Let G = ( V , E ) be an arbitrary graph. If the subgraph G ′ = ( V , E ∖ X ) is connected for all X ⊆ E  where | X | < k , then G is said to be k-edge-connected. The edge connectivity of G is the maximum value k such that G is k-edge-connected. The smallest set X whose removal disconnects G is a minimum cut in G. 

in other words, Given a connected graph G=(V,E), the **edge connectivity** **λ(G)** is defined as the smallest number of edges whose removal results in a disconnected graph. In other words, it's the size of the smallest edge cut that s**eparates the graph into two or more disconnected components**.

**Example:**
Consider a simple triangle graph with three vertices connected by three edges. Removing any single edge from this graph will still leave the graph connected, but removing two edges will disconnect it. Therefore, the edge connectivity of this triangle graph is 2.

Suppose we have the following graph:
![[Pasted image 20250205113603.png]]

If we remove edges e1 and e5 then the graph becomes disconnected, thus the edge connectivity of this graph is 2.
![[Pasted image 20250205113745.png]]

