In graph theory, **edge connectivity** refers to the minimum number of edges that must be removed from a connected graph to disconnect it. 

This concept is crucial for understanding the resilience of networks, as it indicates how many edges can be removed before the network becomes disconnected.

**Formal Definition:**
Let G = ( V , E ) ![{\displaystyle G=(V,E)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/644a8d85ee410b6159ca2bdb5dcb9097e2c8f182) be an arbitrary graph. If the [subgraph](https://en.wikipedia.org/wiki/Glossary_of_graph_theory#Subgraphs "Glossary of graph theory") G ′ = ( V , E ∖ X ) ![{\displaystyle G'=(V,E\setminus X)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9596f609a5adf1ff1eca5906350467c4bd36db19) is connected for all X ⊆ E ![{\displaystyle X\subseteq E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d967e85b6b85d3d57728fb376536c9a7718759e4) where | X | < k ![{\displaystyle |X|<k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5648352e2d1b8f41bf713752d2f7159cc5889519) , then _G_ is said to be _k_-edge-connected. The edge connectivity of G ![{\displaystyle G}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5f3c8921a3b352de45446a6789b104458c9f90b) is the maximum value _k_ such that _G_ is _k_-edge-connected. The smallest set _X_ whose removal disconnects _G_ is a [minimum cut](https://en.wikipedia.org/wiki/Minimum_cut "Minimum cut") in _G_.

Given a connected graph G=(V,E), the **edge connectivity** **λ(G)** is defined as the smallest number of edges whose removal results in a disconnected graph. In other words, it's the size of the smallest edge cut that s**eparates the graph into two or more disconnected components**.

**Example:**
Consider a simple triangle graph with three vertices connected by three edges. Removing any single edge from this graph will still leave the graph connected, but removing two edges will disconnect it. Therefore, the edge connectivity of this triangle graph is 2.

