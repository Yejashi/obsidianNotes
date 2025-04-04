### Question 1
Graph isomorphism is a structure-preserving bijection. $G$ is isomorphic to $H$ whenever there exists a bijection f : V (G) → V (H) such that vertices u and v are adjacent in G if and only if f (u) and f (v) are adjacent in H.
1. Produce the largest planar graph you can find that is isomorphic to its own geometric dual.
   ![[Pasted image 20250312134316.png]]
   Planar graphs that have the same number of faces as vertices seem to always produce isomorphic geometric duals.

2. Characterize graphs that are isomorphic to their own line graphs.
   ![[Pasted image 20250312135412.png]]
   Cycle graphs ($C_n$) with $n >= 3$ are always isomorphic to their own line graphs.

3. Determine if there exists a planar graph that is isomorphic to both its geometric dual and its line graph. Justify your answer.
   It's not possible for a planar graph to be isomorphic to both its geometric dual and its line graph because a self-dual graph must have an equal number of vertices and faces, which limits its structure. For a graph to be isomorphic to its line graph, it must have a very specific degree pattern that regular graphs like cycles and cliques follow. Since no planar graph can meet both the dual and line graph conditions simultaneously, such a graph doesn't exist.
### Question 2
Find a valid tree-decomposition of the following graph. What is the treewidth of the
graph?
![[Pasted image 20250312123144.png]]

![[Pasted image 20250312153906.png]]