Depth-first search (DFS) is an algorithm used to traverse or search through tree or graph data structures. Starting from a root node, it explores as far as possible along each branch before backtracking, utilizing a stack to keep track of nodes along the current path.

**Key Properties:**
- **Time Complexity:** For explicit graphs traversed without repetition, the time complexity is O(|V| + |E|), where |V| is the number of vertices and |E| is the number of edges. For implicit graphs with branching factor _b_ searched to depth _d_, the complexity is O(b^d).
- **Space Complexity:** If the entire graph is traversed without repetition, the space complexity is O(|V|). For implicit graphs without elimination of duplicate nodes, it is O(bd), where _b_ is the branching factor and _d_ is the depth.
- **Completeness:** DFS is complete unless infinite paths are possible.
- **Optimality:** DFS is not generally optimal, as it does not necessarily find the shortest path.


**Example:**
Consider a graph where a DFS starting at node A, assuming left edges are chosen before right edges and previously visited nodes are remembered, will visit nodes in the order: A, B, D, F, E, C, G. The edges traversed form a Trémaux tree, a structure with important applications in graph theory.