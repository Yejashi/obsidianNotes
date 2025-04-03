Perfect. I’ll get started on creating an extremely detailed, topic-structured study guide that incorporates everything from your notes and all three past exams. It will cover all the major topics with deep explanations and relevant practice questions to make sure you're well-prepared.

I’ll let you know as soon as the guide is ready for you to review.

# Comprehensive Algorithms Exam Study Guide

## Greedy Algorithms

Greedy algorithms build a solution step by step, always choosing the option that looks best at the moment. The key property of a greedy approach is that it **never reconsiders earlier choices**, assuming that local optima will# Comprehensive Algorithms Exam 2 Study Guide

## Greedy Algorithms

A **greedy algorithm** builds a solution piece by piece, always choosing the option that looks best at the moment. The key property is that it **never backtracks** on choices – it assumes that picking a local optimum at each step will lead to a global optimum. Greedy algorithms are usually fast and simple, but they don’t always produce the optimal solution for every problem (counterexamples exist when the greedy-choice property fails). However, for many optimization problems that **do** satisfy the greedy-choice property and optimal substructure, a greedy strategy yields an optimal solution.

**Example – Huffman Coding:** Huffman’s algorithm is a classic greedy method to construct an **o (notes.pdf) code** (variable-length binary encoding for characters) for data compression. The goal is to assign shorter bit codes to more frequent characters and longer codes to less frequent characters, minimizing the weighted average code length. Huffman coding works by repeatedly **greedily combining** the two least-frequent symbols:

1. Start with all characters as separate nodes weighted by frequency.
    
2. Repeatedly pick the two lowest-frequency nod (notes.pdf)m into a new node with weight equal to their sum (this forms a binary tree structure).
    
3. Continue until a single tree remains. Assign 0/1 to left/right branches.
    

**Correctness:** Huffman’s greedy merges produce an optimal coding tree (it can be proven by exchange arguments). This (notes.pdf) space depending on frequency distribution.

_Huffman tree constructed for characters A,B,C,D,E,F with frequencies 5,9,12,13,16,45 (more frequent chars end up nearer the root). Internal nodes are labeled by combined frequencies._

Each leaf in the Huffman tree above represents a character and its code (e.g., F, with highest frequency 45, ended up with the shortest code). The greedy merging ensured the tree has minimal weighted path length. For (notes.pdf)g the tree: `F → 0; C → 100; D → 101; A → 1100; B → 1101; E → 111`. No code is a prefix of another (prefix-free property), so the encoding is unambiguous.

Another example (exam2_1.pdf)orithms on graphs is **Minimum Spanning Tree**. Both Prim’s and Kruskal’s algorithms build an MST greedily:

- _Prim’s Algorithm:_ Start from an arbitrary node and grow the tree by always adding the smallest weight edge that connects a new vertex to the tree. This uses a priority queue to pick the next mini (exam2_1.pdf)of the “frontier” of the current tree.
    
- _Kruskal’s Algorithm:_ Sort all edges by weight (notes.pdf)through them, adding an edge to the spanning tree if it doesn’t create a cycle. This uses the Union-Find data structure to efficiently detect cycles.  
    Both run in O(Elog⁡V)O(E \log V) time due to sorting or priority queues and correctly produce an MST (they are greedy but can be proven optimal by the cut property of MSTs).
    

Greedy methods also appear in shortest-path algorithms. **Dijkstra’s algorithm** is greedy: it picks the closest un (notes.pdf)ex at each step to permanently set its distance (this works only for non-negative edge weights). By always choosing the next shortest tentative distance, Dijkstra’s achieves the single-source shortest paths in O((V+E)log⁡V)O((V+E)\log V) time.

> **Practice Question (Greedy):** Construct an optimal Huffman code for characters `X, Y, Z, W` with frequencies 2, 3, 5, 10. Show the coding tree and codes.

**Solution:** Combine the lowest frequencies greedily. Here are the steps:

- Lowest two frequencies: 2 (`X`), 3 (`Y`). Merge them (weight 5).
    
- Now weights: 5 (m (exam2_1.pdf)5 (`Z`), 10 (`W`). Merge the two 5s (`X+Y` node with `Z`) to get a node of weight 10.
    
- Now merge 10 (from `X,Y,Z`) with 10 (`W`) to get root weight 20.
    

The Huffman tree (exam2_1.pdf)erge(`X`,`Y`) forms one subtree, `Z` is another leaf, and `W` is the other leaf. One optimal code assignment is: `W = 1` (single bit since W had highest freq), `Z = 00`, `X = 010`, `Y = 011`. The exact codes may differ by swapp (notes.pdf)ntions, but lengths should reflect frequencies (e.g. `W` gets 1-bit code, less frequent ones get longer codes). This is the optimal prefix-free code given the frequencies.

## Dynamic Programming

**Dynamic Programming (DP)** is an algorithm design paradigm that is useful for optimization problems with **overlapping subproblems** and **optimal substructure**. In DP, we break a problem into subproblems, solve each subproblem once, and store their solutions – typically using a table – so that we do not recompute them later. This technique is often implemented either bottom-up (tabulation) or top-down (memoization).

- In contrast to greedy algorithms which make a **myopic choice**, DP systematically explores all possibilities (but prunes redundant computations through reuse of solutions). It is essentially a careful brute-force that avoids recomputation.
    
- A classic example: computing Fibonacci numbers. A naive recursive approach does exponential work due to recomputation, but using DP (ca (notes.pdf)) computes F(n)F(n) in O(n)O(n) time by building up from base cases.
    
- Another example: **Knapsack problem (0/1)** – DP can fill a table of size (items × capacity) to find the optimal value, since the problem can be broken into subproblems defined by smaller capacities or fewer items.
    

The **time complexity** of a DP solution is often the product of the number of subproblems and the time to solve each subproblem. For example, if a DP has nn stages and at each stage there are dd possible decisions, the total subproblems = n×dn \times d, and solving each in O(1) leads to O(n⋅d)O(n\cdot d) time.

> **Practice Question (DP):** An algorithm uses DP on an _n_-stage decision process, each stage with _d_ possible decisions. What is the time complexity to evaluate the optimal solution with DP?

**Solution:** It would be O(n×d)O(n \times d). The DP would typically evaluate (exam2_3.pdf) each possible decision (combining solutions of previous stage), a total of nn×dd (exam2_3.pdf)aluations (assuming O(1) work per subproblem). For example, if n=5n=5 stages and d=10d=10 decisions each, about 50 subproblem states are considered (which is far more efficient than brute-forcing 105=100,00010^5 = 100,000 sequences of decisions).

*(In general, DP complexity = number of states × transitions per state. Here number of states = nn (stage index) times possibly some state variable for previous decisions – but since each stage is independent with d choices, it’s simply ( (exam2_1.pdf)

## Graph Algorithms

Graphs are a fundamental structure. We review graph representations, traversal algorithms (BFS/DFS), topological sort, connectivity, and shortest paths, as well as greedy tree algorithms (MST).

**Graph Representations:** Common ways to represent a graph with VV vertices and EE edges:

- **Adjacency Matrix:** a V×VV \times V matrix where entry [i][j][i][j] is 1 if there's an edge from i to j (or the weight if weighted). Uses O(V2)O(V^2) space, which is fine for dense graphs.
    
- **Adjacency List:** for each vertex, store a list of outgoing (or incoming) neighbors. Uses O(V+E)O(V + E) space, efficient for sparse graphs.
    
- **Incidence Matrix:** a V×EV \times E matrix, rows = vertices, columns = edges, with 1s indicating which vertices are incident on each edge (useful in some theoretical contexts).
    

### BFS and DFS (Graph Traversal)

**Breadth-First Search (BFS):** explores the graph level by level from a start vertex. It uses a queue to visit all neighbors of the start vertex, then neighbors of those neighbors, and so on. BFS finds the shortest path (in terms of number of edges) from the start vertex to all others in an _unweighted_ graph. It also can detect connected components. In a BFS tree (or forest), edges not in the tree that connect a node to an already visited node will always connect nodes across the same or adjacent levels. In an undirected graph, BFS tree **may have cross-edges** (between nodes at the same level), but it will not have back-edges that go to an earlier level because BFS spans outward level by level.

**Depth-First Search (DFS):** explores deeply: it goes from the start vertex down one path as far as po (exam2_1.pdf)backtracks. It uses a stack (implicitly via recursion) to manage exploration. DFS can be used to classify edges by their relationship in the DFS tree:

- **Tree edges:** those used in the DFS spanning tree.
    
- **Back edges:** edges that connect a vertex to an **ancestor** in the DFS tree (backwards in (exam2_1.pdf)-L47】. The presence of a back edge indicates a cycle in the graph. In directed graphs, back edges mean the graph is not a DAG.
    
- **Forward edges:** edges that connect a vertex to a descendant in the DFS tree (these can only occur in directed graphs).
    
- **Cross edges:** edges conn (notes.pdf)in different branches of the DFS tree, neither in ancestor-descendant relationship. In **undirected graphs, DFS won’t have cross edges** – any non-tree edge will be a back edge because undirected edges connect nodes that are ancestors/descendants in DFS tree. In directed graphs, cross edges can occur (e.g., between different DFS subtrees), but they typically don’t indicate cycles.
    

DFS is useful for **cycle detection** (via back edges), **topological sorting** (ordering nodes of a DAG via DFS finish times), and finding connectivity. Its time complexity is O(V+E)O(V+E). BFS is also O(V+E)O(V+E).

**Topological Sort:** This is an order (exam2_1.pdf)es in a directed acyclic graph (DAG) such that each edge u→vu \to v goes from earlier to later in the order. A DFS-based algorithm can produce a topological sort by performing DFS and placing each node on a stack when finished (or outputting in reverse finish time order). Alternatively, Kahn’s algorithm (greedy) repeatedly removes nodes with no incoming edges. Topological sorting is only possible if the graph has no cycles (i.e., it’s a DAG), and a cycle detection during DFS can signal if no topological order exists. Use cases include ordering of tasks given prerequisites, resolving build dependencies, etc..

**Connectivity:** For undirected graphs, both BFS and DFS can find **connected components**: if you start a traversal at an unvisited node and mark all reachable nodes, that set is one connected component. For directed graphs, one can find *_strongly connect (exam2_3.pdf)_ (SCCs) using algorithms like Kosaraju’s or Tarjan’s (based on DFS). Connectivity can also be quantified in terms of **edge connectivity** (minimum edges whose removal disconnects the graph) or **vertex connectivity** (min vertices whose removal disconnects the grap (exam2_3.pdf)be determined with more advanced techniques (e.g., using max-flow for edge connectivity as discussed later).

> **Practice Question (DFS):**  
> a. What is a **back edge** in (exam2_3.pdf)s it useful?  
> b. What is a **cross edge** in DFS, and how is it treated?

**Solution:**  
a. A back edge is an edge from a node back to one of its **ancestors** in the DFS tree (e.g., an edge v→uv \to u where uu discovered earlier and is an ancestor of vv in the DFS recursion stack). Back edges indicate the presence of a cycle – if a DFS finds a back edge, it means we can go from the ancestor down to the current node via tree edges and then back up, forming a cycle. Algorithmically, back edges are used in cycle detection and in finding strongly connected components. In an undirected grap (exam2_3.pdf)e edge is by definition a back edge (since the graph being undirected means the two endpoints are connected through the tree plus this edge, forming a cycle). In directed graphs, back edges are one type of edge (distinct from cross and forward edges) identified in a DFS edge classification.

b. A cross edge is an edge that connects two nodes that have no ancestor-descendant relationship in the DFS forest. In other words, it goes between two separate DFS tree branches or from a node to another that wa (exam2_3.pdf)_earlier but is not its ancestor_*. Cross edges can only occur in directed graphs (in undirected graphs, such an edge would actually be a back edge due to the undirected nature). Cross edges do not indicate cycles (they go between parallel branches), and they are generally not “useful” for DFS beyond showing an alternate connection. In a DFS tree of an undirected graph, **cross edges don’t appear** (because any edge connecting to a previously visited node in an undirected graph connects to an ancestor, hence a back edge). In directed graphs, cross edges might connect nodes at the same DFS depth or across subtrees – they can be used in algorithms like topological sorting (they will always go from higher order to lower order in a topological sort of a DAG).

### Minimum Spanning Tree (MST)

An MST of a weighted graph is a subset of edges that connects all vertices with minimum possible total weight. Applications include network design (least expensive wiring connecting all sites), clustering (an MST can be cut to form clusters), etc. Two greedy MST algorithms were already mentioned:

- **Kruskal’s Algorithm:** Sort edges by weight (smallest to largest), initialize an empty forest, then iterate through sorted edges adding each edge if it doesn’t form a cycle. Use Union-Find (disjoint set union) to efficiently check connectivity and avoid cycles. Stop when you have added V−1V-1 edges and formed a spanning tree.  
    _Correctness:_ Follows from the **cut property** – at each step, a minimum-weight edge crossing any partition (cut) of the vertices is guaranteed to be in some MST. Kruskal’s picks such edges globally.
    
- **Prim’s Algorithm:** Start from an arbitrary vertex and grow a tree. At each step, add the cheapest edge from the tree to a new vertex not yet in the tree. Use a min-heap to select the next minimum edge out of the current tree (similar to Dijkstra’s procedure for distances, but here the “distance” is the cost of an edge to connect a new vertex). Repeat until all vertices are included.  
    _Correctness:_ Follows from the **cut property** as well – Prim’s always adds a globally light edge from the tree to the rest.
    

Both algorithms yield an MST with total weight optimal. They run in O(Elog⁡V)O(E \log V) time in practice (dominantly from sorting edges or extracting from a min-heap). MST algorithms illustrate that a greedy approach (choosing the locally smallest edge) can achieve a globally optimal solution, thanks to the structure of the spanning tree problem.

### Shortest Paths in Graphs

For unweighted graphs (or equal-weight edges), **BFS** from a source finds shortest path distances (in number of edges) to every reachable vertex. For weighted graphs, the classic algorithms are:

- **Dijkstra’s Algorithm:** Computes single-source shortest distances when all weights are non-negative. It uses a greedy strategy – at each step, pick the not-yet-finalized vertex with the smallest tentative distance, finalize it, and relax its outgoing edges. Initially, distance to source = 0, others = ∞. Using a min-priority queue, each vertex is finalized exactly once, and all edges are relaxed. Runs in O((V+E)log⁡V)O((V+E)\log V). Dijkstra’s fails if negative edge weights exist (as greedy choice can be wrong in that case).
    
- **Bellman–Ford Algorithm:** Handles graphs with negative edge weights (but no negative cycles reachable from the source). It relaxes all edges repeatedly in passes. After at most V−1V-1 passes, shortest distances are found (if no negative cycle). It runs in O(V⋅E)O(V \cdot E) time. If a further pass still improves a distance, a negative cycle is detected. Bellman–Ford is useful for situations like currency exchange arbitrage detection or as a subroutine in more complex algorithms.
    
- **Floyd–Warshall Algorithm:** A dynamic programming algorithm for **all-pairs shortest paths**. It runs in O(V3)O(V^3) time and can handle negative weights (but no negative cycles). It works by iterative improvement, considering intermediate vertices one by one. Floyd–Warshall is good for dense graphs or moderate vertex counts (up to a few hundred).
    

Together, these algorithms cover typical shortest-path problems. For instance, computing driving distances on a road network (non-negative weights) would use Dijkstra’s or its variants. If edge weights can be negative (but no cycles), Bellman–Ford is the fallback. For exhaustive distance matrices or determining the diameter of small graphs, Floyd–Warshall is appropriate.

## Network Flow

A **flow network** is a directed graph where each edge (u→v)(u \to v) has a nonnegative **capacity** c(u,v)c(u,v). We designate a **source** node ss where flow originates and a **sink** node tt where flow terminates. A **flow** assigns a value f(u,v)f(u,v) to each directed edge such that it satisfies:

- **Capacity constraint:** 0≤f(u,v)≤c(u,v)0 \le f(u,v) \le c(u,v) for all edges (can’t exceed capacity).
    
- **Skew symmetry:** flow in reverse direction is the negative of forward flow, i.e. f(u,v)=−f(v,u)f(u,v) = -f(v,u). (Often one just tracks flow in one direction and implicitly defines opposite flow for bookkeeping.)
    
- **Flow conservation:** For every vertex except ss and tt, total inflow = total outflow. In other words, ∑wf(w,v)=∑wf(v,w)\sum_{w} f(w, v) = \sum_{w} f(v, w) for all intermediate vertices vv.
    

The **value** of a flow is the net flow out of the source (which is equal to net flow into the sink). The **Maximum Flow Problem** is: find the largest possible flow value from ss to tt without violating capacities.

**Augmenting Paths and Ford–Fulkerson:** The foundational algorithm for max flow is to repeatedly find an **augmenting path** – a path from ss to tt in the current **residual graph** (graph of remaining capacities) – and push flow along it. The residual capacity of an edge is c(u,v)−f(u,v)c(u,v) - f(u,v) (how much more can be sent) and for flow already sent, a reverse edge in residual allows cancellation if needed. Ford–Fulkerson steps:

1. Start with zero flow.
    
2. While an ss-tt path exists in the residual network, send as much flow as possible (the **bottleneck** capacity) along that path.
    
3. Update residual capacities (subtract bottleneck on forward edges, add on reverse edges) and repeat.
    

Each augmentation increases the flow value. If path choice is unlucky, this process can in theory run indefinitely (if flows keep getting augmented by tiny amounts – the classic example with irrational capacities). But if using specific strategies like **Edmonds–Karp** (which chooses the shortest augmenting path in terms of number of edges, i.e. BFS in residual graph), the algorithm runs in O(V⋅E2)O(V \cdot E^2) time and guarantees termination.

A remarkable theorem in network flow is the **Max-Flow Min-Cut Theorem:** The maximum value of an ss-tt flow equals the minimum capacity of an ss-tt cut (a cut is a partition of vertices with ss and tt separated; its capacity is sum of capacities of edges going from the ss-side to the tt-side). This establishes that augmenting until no path remains in residual (i.e., we’ve saturated some cut) indeed finds the optimal flow.

**Applications of Max Flow:** Network flow is a versatile tool that can model many problems by constructing appropriate flow networks:

- **Bipartite Matching:** Given a bipartite graph (left set UU, right set VV; edges only between UU and VV), we can find a maximum matching (largest set of edges with no shared endpoints) by flow. Construct a source connected to all left nodes (capacity 1 each), connect all right nodes to the sink (capacity 1), and give each original edge u∈U→v∈Vu\in U \to v\in V capacity 1. A max flow in this network (with integer capacities) will send 1 unit along edges corresponding to a matching. Because of capacity-1, flow can’t send more than 1 unit through a node, effectively matching it at most once. The value of the max flow = size of maximum matching. This reduction transforms matching into max flow, solvable in O(EV)O(E \sqrt{V}) with Dinic’s algorithm or similar in practice.
    
- **Edge Connectivity / Network Reliability:** To find the minimum number of edges whose removal disconnects two vertices (say aa and bb) – also known as the edge connectivity between aa and bb – we can compute a max flow treating each edge capacity as 1. The min cut found (by max-flow min-cut) gives the smallest set of edges that separates aa and bb. By running flows between various pairs (or using more sophisticated global minimum cut algorithms), one can find the overall edge connectivity of a graph (the minimum over all pairs). Similarly, **vertex connectivity** can be computed by transforming vertices to edges (split each vertex into in/out with an edge of capacity 1 between).
    
- **Circulation problems and others:** Flow algorithms can solve problems like scheduling with disjoint paths, circulation with demands, finding disjoint paths, etc., by adding lower bound demands or modifying the network appropriately.
    
- **Feasible 0-1 Matrix with given row/column sums:** This is a specific application: _Given desired row sums r1,…,rmr_1,\dots,r_m and column sums c1,…,cnc_1,\dots,c_n, can we fill an m×nm \times n binary matrix with 0/1 such that each row ii has rir_i ones and each column jj has cjc_j ones?_ We can model this as a flow problem:
    
    - Create a source ss connecting to each row node ii with capacity rir_i.
        
    - Connect each column node jj to the sink tt with capacity cjc_j.
        
    - Connect each row node to each column node with capacity 1 (each cell can contribute at most one “1”).
        
    - Now, if there is a flow that saturates all the row->source and column->sink edges (total flow = total number of 1s needed = ∑ri=∑cj\sum r_i = \sum c_j), then such a matrix exists. The flow will effectively assign ones to specific row-column pairs.
        
    
    If max flow < total sum, no such matrix exists (it’s impossible to satisfy those marginals).
    

> **Practice Question (Flow):** Using max flow, determine whether a 3×3 binary matrix with **row sums** (2, 1, 1) and **column sums** (1, 1, 2) exists. If yes, provide one such matrix.

**Solution:** The total number of 1s required is 2+1+1 = 4 (also 1+1+2 = 4, so totals match, a necessary condition). We set up a flow with source→row capacities [2,1,1] and column→sink capacities [1,1,2]. A possible flow assignment is:

- Row1 sends 1 to Col1 and 1 to Col2.
    
- Row2 sends 1 to Col3.
    
- Row3 sends 1 to Col3.
    

This yields the matrix (Row × Col):

```
1  1  0
0  0  1
0  0  1
```

Row sums = [2,1,1] and Col sums = [1,1,2] as desired. The flow algorithm would find this assignment. (Indeed, max flow = 4 which equals the total required, so a valid matrix exists.) There are other solutions too; for instance, Row3’s “1” could go to Col1 instead and Row1’s second “1” to Col3 – yielding:

```
1 0 1
0 0 1
1 0 0
```

which also meets (2,1,1)/(1,1,2).

_(This kind of bipartite flow model is essentially the “Hall’s theorem” check for a valid bipartite matching between row slots and column slots of 1s.)_

## Linear Programming (LP)

A **Linear Program** is an optimization problem where we seek to maximize or minimize a linear objective function subject to a set of linear constraints (equalities or inequalities) on the decision variables. A canonical form is:

Maximize cTxc^T x subject to Ax≤bA x \le b, and x≥0x \ge 0, where xx is a vector of variables. This is a **linear objective** and **linear constraints**. Any LP can be transformed into an equivalent form. For instance, “≤” constraints can be converted to “=” by adding **slack variables** (to represent unused capacity), and ≥ constraints use surplus variables, etc. There is also a **Standard Form** (all constraints as equalities with slack/surplus, and all variables ≥0) and a **Dual** LP associated with every LP, but for exam focus the key is understanding the solution methods.

**Feasible solution:** any assignment to xx satisfying all constraints (within the polyhedron defined by Ax≤bAx \le b).  
**Optimal solution:** a feasible solution that achieves the best objective value (max or min). If no feasible solution exists, the LP is **infeasible**; if the objective can grow without bound, the LP is **unbounded**.

LPs have the important property that if an optimal solution exists, there is an optimal **basic** solution at a **vertex (corner point)** of the feasible region polytope. This is why the classic solving method, the **Simplex algorithm**, focuses on corner-point solutions. Simplex moves from one corner of the feasible region to an adjacent corner with a better objective, and so on, until optimal is reached.

**Simplex Algorithm (outline):**

- Convert the LP to slack form (introduce slack variables for “≤” inequalities, converting them to equalities). Identify an initial basic feasible solution (usually, set decision variables to 0 and let slacks = RHS of constraints).
    
- At each iteration, **check the objective row** for improving directions: find a non-basic variable with a positive coefficient in the objective (for maximization) – this variable if increased will improve the objective. Choose the one with the largest coefficient (greedy choice for fastest improvement). This is the **entering variable**.
    
- Increase this entering variable from 0 upwards – as we do so, some constraints (basic variables) will start to decrease (since we satisfy the equalities). Find the **limiting constraint** that restricts how much we can increase the entering variable (compute ratio of current RHS to the coefficient of entering var in each constraint). The smallest ratio gives the **leaving variable** (the basic variable that hits zero first and will leave the basis). This is essentially moving to an adjacent corner of the polytope.
    
- **Pivot:** Solve the linear equations to make the entering variable basic and the leaving variable non-basic (update the tableau). This updates all equations (this can be done systematically with Gauss-Jordan elimination steps).
    
- Repeat: now with a new basic solution (hopefully with improved objective). Continue until **no positive coefficients** in the objective row (for max problem) – meaning you can’t improve further. Then you have reached the optimal corner. The simplex algorithm will terminate with an optimal solution (if the LP is bounded and feasible). It’s guaranteed that objective improves each pivot (or we detect degeneracy or alternate optima which can be handled separately).
    

Despite worst-case exponential time in theory, the simplex method is very efficient in practice for most problems. There are also **Interior-Point Methods** (e.g., Karmarkar’s algorithm) that run in polynomial time and approach the optimum through the interior of the feasible region (as opposed to hopping between vertices). Interior-point methods are useful for very large linear programs where simplex might stall.

> **Practice Question (Simplex):** Solve the following linear program using the simplex method:  
> Maximize Z=3x1+x2Z = 3x_1 + x_2  
> Subject to:  
>   4x1+x2≤84x_1 + x_2 \le 8  
>   x1+x2≤5x_1 + x_2 \le 5  
>   x1,x2≥0.x_1, x_2 \ge 0.  
> Find the optimal values of x1,x2x_1, x_2 and ZZ.

**Solution:** First introduce slack variables s1,s2s_1, s_2 for the two constraints:

```
4x_1 + x_2 + s_1 = 8   -- (1)
x_1  + x_2 + s_2 = 5   -- (2)
Objective:  Z = 3x_1 + x_2. 
```

Initial basic feasible solution: x1=0,x2=0x_1=0, x_2=0, with s1=8,s2=5s_1=8, s_2=5. Initial tableau:

|Basis|x₁|x₂|s₁|s₂|RHS|
|---|---|---|---|---|---|
|s₁ (eq1)|4|1|1|0|8|
|s₂ (eq2)|1|1|0|1|5|
|Z|-3|-1|0|0|0|

_(We put negative of objective coeffs in the tableau for convenience – indicating how much objective improves if we increase that var.)_

- **Iteration 1:** Look at objective row: x1x_1 has coefficient -3, x2x_2 has -1. A negative in the objective row means increasing that variable will improve Z. x1x_1 has the most negative (−3), so choose x1x_1 to enter the basis. Now determine leaving variable by smallest ratio test: For each constraint, RHS/coef of x₁ = (8/4 = 2) for eq1, (5/1 = 5) for eq2. The smaller is 2 (eq1), so s1s_1 leaves the basis. We pivot on x1x_1 in eq1.
    

After pivot, eq1 becomes x1=2−0.25x2−0.25s1x_1 = 2 - 0.25x_2 - 0.25s_1 (dividing by 4 and expressing in terms of nonbasics). Substituting into eq2: 2−0.25x22 - 0.25x_2 for x1x_1 in eq2 gives 2−0.25x2+x2+s2=52 - 0.25x_2 + x_2 + s_2 = 5 ⇒ 0.75x2+s2=30.75x_2 + s_2 = 3 ⇒ s2=3−0.75x2s_2 = 3 - 0.75x_2. The new basic equations are:

```
x_1 = 2 - 0.25 x_2 - 0.25 s_1   (now x₁ is basic)
s_2 = 3 - 0.75 x_2 + 0.0 s_1   (s₂ remains basic)
```

and Z=6+0.75x2+0.75s1Z = 6 + 0.75 x_2 + 0.75 s_1 (we recompute Z: originally 0, now Z = 3*2 = 6 plus contributions of nonbasics). Updated tableau:

|Basis|x₁|x₂|s₁|s₂|RHS|
|---|---|---|---|---|---|
|x₁|1|0.25|0.25|0|2|
|s₂|0|0.75|-0.25|1|3|
|Z|0|0.75|0.75|0|6|

Now x1=2,x2=0x_1=2, x_2=0 (solution (2,0) with Z=6).

- **Iteration 2:** Objective row: x2x_2 has coefficient +0.75 (positive, meaning if we increase x2x_2, objective increases). So x2x_2 enters. Ratio test for x2x_2: in eq1, coefficient 0.25 → RHS 2 / 0.25 = 8; in eq2, coefficient 0.75 → 3 / 0.75 = 4. The smaller is 4 (eq2), so s2s_2 leaves. Pivot on x2x_2 in eq2. Eq2 becomes x2=4+13s1−43s2x_2 = 4 + \frac{1}{3}s_1 - \frac{4}{3}s_2 (from 0.75x2+s2=30.75x_2 + s_2 = 3). Substitute into eq1: x1=2−0.25(4+13s1)=2−1−112s1=1−112s1+1?s2x_1 = 2 - 0.25(4 + \frac{1}{3}s_1) = 2 - 1 - \frac{1}{12}s_1 = 1 - \frac{1}{12}s_1 + \frac{1}{?}s_2 (since s2s_2 dropped out from eq1 which had none). Simplifying, we get final basic solution:
    

```
x_1 = 1
x_2 = 4
```

with s1=0,s2=0s_1 = 0, s_2 = 0 and objective Z=3∗1+1∗4=7Z = 3*1 + 1*4 = 7. This is optimal because now in the objective row all coefficients of non-basics are non-positive (or we can see we’ve hit the constraint boundaries). Indeed, the feasible region polygon had corners at (0,0), (0,5), (2,0), and (1,4); the last is the optimum giving Zmax⁡=7Z_{\max} = 7.

Thus, the simplex method yields **x1=1,x2=4x_1 = 1, x_2 = 4 with Zmax⁡=7Z_{\max} = 7**.

_(Note: You could also solve this by reasoning about constraints: the intersection of 4x1+x2=84x_1+x_2=8 and x1+x2=5x_1+x_2=5 gives (1,4) which indeed lies in the feasible region and yields the highest value 7 among all corner points. Simplex systematically arrived at the same result.)_

## Polynomial Multiplication & Fast Fourier Transform (FFT)

Multiplying two polynomials of degree n−1n-1 (with nn terms) directly is an O(n2)O(n^2) operation – for each term of the first polynomial you multiply by each term of the second. For large nn, this is slow. The **Fast Fourier Transform** is a divide-and-conquer algorithm that multiplies polynomials (or, equivalently, convolves sequences) in **O(nlog⁡n)O(n \log n)** time, which is a drastic improvement.

The main idea is to evaluate both polynomials at enough points, multiply the results pointwise, and then interpolate the product polynomial. Specifically, FFT uses the roots of unity (complex nnth roots of 1) as evaluation points, because they have special symmetry properties that allow an efficient divide-and-conquer evaluation and interpolation.

**Key ideas:**

- A polynomial A(x)A(x) of degree < nn can be split into **even** and **odd** parts:  
    A(x)=Aeven(x2)+x⋅Aodd(x2)A(x) = A_{\text{even}}(x^2) + x \cdot A_{\text{odd}}(x^2).  
    For example, if A(x)=a0+a1x+a2x2+a3x3A(x) = a_0 + a_1 x + a_2 x^2 + a_3 x^3, then Aeven(y)=a0+a2yA_{\text{even}}(y) = a_0 + a_2 y and Aodd(y)=a1+a3yA_{\text{odd}}(y) = a_1 + a_3 y such that A(x)=Aeven(x2)+x⋅Aodd(x2)A(x) = A_{\text{even}}(x^2) + x \cdot A_{\text{odd}}(x^2).
    
- The nn complex nth roots of unity (points ωk\omega^k for k=0,...,n−1k=0,...,n-1, where ω=e2πi/n\omega = e^{2\pi i/n}) have the property that ωn/2=−1\omega^{n/2} = -1, ωn=1\omega^n = 1. Using these, FFT evaluates the polynomial at these points in a recursive manner. Because of the even/odd split, we only need to evaluate the two half-size polynomials AevenA_{\text{even}} and AoddA_{\text{odd}} at the **n/2** distinct points ω0,ω2,ω4,...\omega^0, \omega^2, \omega^4, ... (the even powers) and reuse those results to get evaluations at the odd powers as well. This halves the work recursively. The symmetry here is that evaluating at ωk\omega^k and ωk+n/2=−ωk\omega^{k+n/2} = -\omega^k shares a lot of the computation.
    
- By recursively splitting, the FFT achieves O(nlog⁡n)O(n \log n) for evaluating a polynomial of size nn at nn points. Similarly, an inverse FFT can interpolate the polynomial from point values in O(nlog⁡n)O(n \log n). Thus, two degree-(n−1)(n-1) polynomials can be multiplied by performing two FFTs (to evaluate each polynomial), multiplying the evaluations pointwise (this is O(n)O(n)), and then doing an inverse FFT to get the coefficients of the product.
    

**Where does symmetry play a role?** At the heart of FFT is the fact that the computations for the first half of the points (ωk\omega^k for k<n/2k < n/2) can be reused for the second half (ωk+n/2=−ωk\omega^{k+n/2} = -\omega^k). Specifically, when combining results of recursive calls, the FFT does computations like: for each kk in 0 to n/2−1n/2-1, compute  
Y[k]=E[k]+ωk⋅O[k],Y[k] = E[k] + \omega^k \cdot O[k],  
Y[k+n/2]=E[k]−ωk⋅O[k],Y[k+n/2] = E[k] - \omega^k \cdot O[k],  
where E[k]E[k] is the evaluation of the even part at ωk\omega^k and O[k]O[k] is the evaluation of the odd part at ωk\omega^k. Here ωk\omega^k serves as the **twiddle factor**. Notice ωk+n/2=−ωk\omega^{k+n/2} = -\omega^k flips the sign in the second formula. This reuse of E[k]E[k] and O[k]O[k] for two results is the symmetry that saves half the operations at each level of recursion. Mathematically, the symmetry is in the sine/cosine values of roots of unity: the FFT is essentially leveraging the identities cos⁡(θ+π)=−cos⁡θ,sin⁡(θ+π)=−sin⁡θ\cos(\theta + \pi) = -\cos\theta, \sin(\theta + \pi) = -\sin\theta. Thus, it doesn’t need to compute those from scratch for the second half.

By exploiting these symmetries, FFT reduces redundant calculations. In summary, the polynomial multiplication via FFT works by performing evaluations and interpolations in a way that each stage halves the problem size (using symmetries of roots of unity), leading to the O(nlog⁡n)O(n \log n) complexity.

> **Practice Question (FFT Concept):** Why can two polynomials of degree nn be multiplied in O(nlog⁡n)O(n \log n) time using the Fast Fourier Transform? Explain how symmetry is used in the FFT algorithm to speed up computation.

**Solution:** The FFT avoids the O(n2)O(n^2) term-by-term multiplication by using the polynomials’ evaluations at carefully chosen points. By evaluating both polynomials at the **n**th roots of unity, multiplying those evaluations pointwise, and interpolating, the multiplication can be done in O(nlog⁡n)O(n \log n). The reason this is efficient is the **divide-and-conquer with symmetry:** when evaluating a polynomial A(x)A(x) at all nnth roots of unity, the polynomial is split into its even and odd parts. Thanks to symmetry of complex roots (specifically ωk+n/2=−ωk\omega^{k+n/2} = -\omega^k), the FFT computes A(ωk)A(\omega^k) for all k in a recursive manner that halves the work at each step. The even polynomial AevenA_{\text{even}} and odd polynomial AoddA_{\text{odd}} are each evaluated at half as many points (the even powers of ω\omega), and the results are then combined using the symmetric properties of the roots of unity (one combination gives A(ωk)A(\omega^k), another gives A(ωk+n/2)A(\omega^{k+n/2}) without a full re-computation). This reuse of computations (exploiting that ωk+n/2\omega^{k+n/2} is just ωk\omega^k times −1-1) is the symmetry that FFT leverages. At each merge step, rather than doing O(n)O(n) work, it does O(n/2)O(n/2) by handling two outputs at once with one set of intermediate values. Recursively, this yields O(nlog⁡n)O(n \log n) total complexity. In short, the symmetry of sine/cosine waves (roots of unity) allows FFT to **double the number of evaluation points at only ~linear cost** each stage, instead of doubling the cost, hence the logarithmic factor in complexity.

## Cryptology and RSA

This section covers basic cryptographic concepts relevant to the exam: the one-time pad, some number theory (modular arithmetic), and the RSA public-key cryptosystem.

**One-Time Pad:** The one-time pad is an encryption technique where a truly random key (a sequence of random bits at least as long as the message) is XORed with the message. It is **provably unbreakable** – the ciphertext provides no information about the plaintext without the key – _provided_ the key is used only once and kept secret. The one-time pad’s impracticality lies in the key: it must be as long as the message and shared securely in advance. Nonetheless, it’s an important theoretical benchmark for perfect secrecy.

**Number Theory Foundations:** Cryptography relies on properties of integers:

- _Divisibility:_ m∣nm \mid n means mm divides nn with no remainder, equivalently n≡0(modm)n \equiv 0 \pmod{m}.
    
- _Prime numbers:_ integers >1 with no positive divisors other than 1 and itself. By the Fundamental Theorem of Arithmetic, every integer factors uniquely into primes. There are infinitely many primes (Euclid’s theorem).
    
- _Modulo arithmetic:_ We write a≡b(modn)a \equiv b \pmod{n} if nn divides a−ba-b. Basic rules: you can add, subtract, and multiply congruences (but division only if the divisor is coprime with modulus).
    
- _Fermat’s Little Theorem:_ If pp is prime and aa is not divisible by pp, then ap−1≡1(modp)a^{p-1} \equiv 1 \pmod{p}. Equivalently, ap≡a(modp)a^p \equiv a \pmod{p}. This is a fundamental property used in RSA and other cryptosystems (actually a special case of Euler’s Theorem, which generalizes to moduli that are not prime).
    

**RSA Algorithm:** RSA is a widely used public-key cryptosystem based on the difficulty of prime factorization. The steps to generate RSA keys are:

1. **Key Generation:** Choose two large prime numbers pp and qq. (These should be random and secret.)
    
2. Compute n=p⋅qn = p \cdot q. nn is the modulus for both the public and private keys. Also compute ϕ(n)=(p−1)(q−1)\phi(n) = (p-1)(q-1) – Euler’s totient of nn (the number of positive integers < n that are coprime with n).
    
3. Choose an **encryption exponent** ee that is coprime with ϕ(n)\phi(n) (i.e., 1<e<ϕ(n)1 < e < \phi(n) and gcd⁡(e,ϕ(n))=1\gcd(e, \phi(n)) = 1). Common choices are small primes like 3, 17, 65537 for efficiency.
    
4. Compute the **decryption exponent** dd as the modular multiplicative inverse of e(modϕ(n))e \pmod{\phi(n)}. That is, find dd such that e⋅d≡1(modϕ(n))e \cdot d \equiv 1 \pmod{\phi(n)}. This can be done via the Extended Euclidean Algorithm.
    
5. The **public key** is (n,e)(n, e) and the **private key** is (n,d)(n, d). (Note: p,q,ϕ(n)p, q, \phi(n) should be kept secret too, as they can be used to find dd.)
    
6. **Encryption:** To send a message MM (as an integer < n), compute the ciphertext C=Me mod nC = M^e \bmod n.
    
7. **Decryption:** Compute M=Cd mod nM = C^d \bmod n. By construction, this recovers the original message because dd was chosen to satisfy Med≡M(modn)M^{ed} \equiv M \pmod{n} for any MM that is relatively prime to nn. In fact, thanks to Euler’s theorem, Mϕ(n)≡1(modn)M^{\phi(n)} \equiv 1 \pmod{n} for MM coprime with nn, and typically ed=1+kϕ(n)ed = 1 + k\phi(n) for some k, so Med=M1+kϕ(n)≡M⋅(Mϕ(n))k≡M(modn)M^{ed} = M^{1+k\phi(n)} \equiv M \cdot (M^{\phi(n)})^k \equiv M \pmod{n}.
    

RSA’s security rests on the assumption that factoring nn into pp and qq is computationally infeasible for large (e.g. 2048-bit) nn. If an attacker could factor nn, they could compute ϕ(n)\phi(n) and then determine dd. Without factoring, given only (n,e)(n, e), recovering dd (or otherwise decrypting messages) is believed to be as hard as factoring.

In practice, RSA requires some padding schemes for security (plain RSA as above is not semantically secure), but those details are beyond the scope of the algorithm itself.

> **Practice Question (RSA):** Consider an RSA system where the primes are p=3p=3 and q=11q=11.  
> a. Compute nn and ϕ(n)\phi(n). Choose a suitable public exponent ee.  
> b. Find the corresponding private exponent dd.  
> c. Encrypt the messages M=4M=4 and M=5M=5 using the public key.  
> d. Which messages in {0,1,…,n−1}\{0,1,\dots,n-1\} cannot be recovered (decrypted) under this RSA setup, and why?

**Solution:**  
a. n=p×q=3×11=33n = p \times q = 3 \times 11 = 33. ϕ(n)=(3−1)(11−1)=2×10=20\phi(n) = (3-1)(11-1) = 2 \times 10 = 20. We need an ee coprime with 20. Let’s choose e=3e = 3 (since gcd⁡(3,20)=1\gcd(3,20)=1). The public key is (n=33,e=3)(n=33, e=3).

b. We need dd such that 3d≡1(mod20)3d \equiv 1 \pmod{20}. By trial or using extended Euclidean algorithm: 3×7=21≡1(mod20)3 \times 7 = 21 \equiv 1 \pmod{20}. So d=7d = 7 works (because 3∗7−1=203*7 - 1 = 20 which is divisible by 20). The private key is (n=33,d=7)(n=33, d=7).

c. Encryption is C=Me mod 33C = M^e \bmod 33.

- For M=4M = 4: C=43 mod 33=64 mod 33=64−33∗1=31C = 4^3 \bmod 33 = 64 \bmod 33 = 64 - 33*1 = 31. So ciphertext is 31.
    
- For M=5M = 5: C=53 mod 33=125 mod 33=125−33∗3=125−99=26C = 5^3 \bmod 33 = 125 \bmod 33 = 125 - 33*3 = 125 - 99 = 26. Ciphertext is 26.
    

So, message 4 encrypts to 31, and message 5 encrypts to 26 under the public key.

We can double-check decryption with d=7d=7: 317 mod 3331^7 \bmod 33 should come out to 4, and 267 mod 3326^7 \bmod 33 should come out to 5 (and indeed they do if you compute them, confirming the correctness of dd).

d. In RSA, encryption and decryption work on the multiplicative group of integers mod nn. If a message MM shares a common factor with nn, i.e. gcd⁡(M,n)≠1\gcd(M,n) \neq 1, then MM is **not coprime with nn** and the standard decrypt formula M=Cd mod nM = C^d \bmod n might not recover the original MM. In this example, n=33=3×11n=33=3 \times 11. Any message that is a multiple of 3 or 11 will cause trouble because Euler’s theorem (and the decryption derivation) assumes Mϕ(n)≡1M^{\phi(n)} \equiv 1 mod nn, which fails if MM is not coprime with nn.

The messages in {0,…,32}\{0,\dots,32\} that are not coprime with 33 are those divisible by 3 or 11: specifically **0, 3, 6, 9, 11, 12, 15, 18, 21, 22, 24, 27, 30, 33** (33 is effectively 0 mod 33). Among these:

- 0 is a trivial case (encrypts to 0, but 0 to the power anything is 0, so decryption gives 0 – actually 0 can be decrypted correctly in this trivial way, but it carries no information).
    
- The message “33” is not in {0,...,32}\{0,...,32\} (we only consider representatives mod 33, so 33 ≡ 0).
    
- The message **11** (which shares a factor 11 with n) will encrypt as 113=1331≡1331 mod 3311^3 = 1331 \equiv 1331 \bmod 33. Note that 1331=11×121=11×(33∗3+22)=11∗(something)+11∗22?Actually,1331mod33=1331−33∗40=1331−1320=11again.1331 = 11 \times 121 = 11 \times (33*3 + 22) = 11*(something) + 11*22? Actually, 1331 mod 33 = 1331 - 33*40 = 1331-1320 = 11 again. Interesting, 11 encrypts to 11 in this case. Decrypting 11 with d=7d=7 gives 117mod3311^7 mod 33. Because 11 is a factor of n, raising it to any power mod 33 will still be a multiple of 11. In fact, 11 raised to any odd power is 11 mod 33, and to any even power is 121 mod 33 = 22 mod 33. So under this RSA, if someone encrypted the message 11, the ciphertext is 11, and decrypting yields 11 – so it actually “round-trips” correctly in this case. But this is more coincidence than RSA working – essentially 11 is a fixed point here. The decryption formula mathematically isn’t guaranteed by the totient theorem when M and n aren’t coprime.
    
- The message **3** (factor 3 with n): 33=27mod  333^3 = 27 \mod 33. Decryption: 277mod  3327^7 \mod 33. 27 is 333^3. Because 3 is a factor, the result will not come back to 3 in general. In fact, you’d get 277=32127^7 = 3^{21}. Since 3’s order mod 33 does not divide 21 nicely (because 3 is of order something 2 maybe?), it will not return to 3. So 3 cannot be uniquely recovered by the RSA inversion process.
    

In simpler terms: **Messages not coprime with n (i.e., 3, 6, 9, 11, 15, 18, 21, 22, 24, 27, 30)** are problematic. They either encrypt to themselves or to some other value that when decrypted does not give the original back (the RSA formula doesn’t guarantee correctness for those). Typically, **0 and any multiples of the prime factors (3 or 11)** are considered “non-invertible” under the RSA transformation. In a properly used RSA, one usually encrypts messages that are smaller than n and often assumes they are integers representing some encoded plaintext that is coprime with n (or uses padding that ensures that).

To give a clear answer: *Messages 0 and 33 (which is effectively 0 mod 33) are... 0 (trivial) and any number sharing a prime factor with 33 (e.g. 3, 11, 22, etc.) cannot be correctly recovered because the RSA decryption relies on the message being coprime with 33. In this case, such messages do not satisfy the conditions of Euler’s theorem. In summary, **messages not coprime with n (like 3 or 11 in this example)** are “unencryptable” in the sense that the standard RSA decryption won’t reliably reproduce the original. (They either encrypt to a value that yields a different plaintext upon decryption or, like 0, yield no information.)

## Complexity Theory (P, NP, NP-Completeness)

**Turing Machines:** A Turing machine is a mathematical model of computation that defines an abstract machine. It consists of an infinite tape (memory) and a head that can read/write symbols and move on the tape according to a set of rules (the machine’s “program”). Despite its simplicity, a Turing machine can simulate any algorithmic computation. If a Turing machine _always halts_ on every input, it decides a language in the class **Recursive** (decidable problems). If it halts on every accepted input (but may loop on others), it recognizes a language in **Recursively Enumerable (RE)**. These formal definitions underpin the theory of what problems can be solved (decided) by algorithms.

**Complexity Classes P and NP:**

- **P** is the class of decision problems (yes/no questions) that can be solved by a deterministic algorithm in **polynomial time** (time nkn^k for some constant kk on inputs of size nn). These are often considered “efficiently solvable” problems (e.g., sorting, shortest path, minimum spanning tree are in P).
    
- **NP** is the class of decision problems for which a given solution (or “certificate”) can be **verified** in polynomial time by a deterministic algorithm. Equivalently, NP is the class of problems solvable by a non-deterministic polynomial-time machine (hence NP = “Nondeterministic Polynomial time”). A common misconception is NP = “not polynomial,” but actually NP **includes** P (any P problem is also in NP – if you can solve it in poly time, you can certainly verify a given solution in poly time). The big open question is whether **P = NP**, i.e., whether every NP problem can be solved as quickly as it can be verified. This is unknown, and is one of the most important unsolved problems in computer science.
    

**NP-hard and NP-complete:**

- A problem XX is **NP-hard** if it’s at least as hard as every problem in NP. Formally, NP-hard means **every** problem in NP can be polynomial-time reduced to XX. NP-hard problems might not be in NP themselves (they could even be undecidable), and they may not be decision problems (could be optimization versions). Intuitively, NP-hard means “at least as hard as the hardest problems in NP.”
    
- A problem YY is **NP-complete** if: (1) YY is in NP, and (2) YY is NP-hard. So NP-complete problems are the “hardest” problems _within_ NP – if you can solve an NP-complete problem in polynomial time, you could solve **every** NP problem in polynomial time (i.e. that would prove P = NP). Conversely, if an NP-complete problem is proven unsolvable in polynomial time, then P≠NP. NP-complete problems are essentially the hardest problems that still belong to NP.
    

**Boolean Satisfiability (SAT):** SAT is the canonical NP-complete problem. SAT asks: given a boolean formula (e.g., in CNF form as a set of clauses, or any logical formula) involving variables {x1,...,xn}\{x_1,...,x_n\}, is there some assignment of true/false values to the variables that makes the formula evaluate to true? For example, F(x1,x2)=(x1∨¬x2)∧(¬x1∨x2)F(x_1,x_2) = (x_1 \vee \neg x_2) \wedge ( \neg x_1 \vee x_2) – is there an assignment to satisfy F? (Yes, x1=true,x2=truex_1=true, x_2=true satisfies this one.) SAT is in NP because given a candidate assignment (the certificate), we can quickly verify by plugging in and checking all clauses evaluate true. SAT was the **first** problem proven NP-complete – the **Cook–Levin Theorem** (1971) showed SAT is NP-complete by reducing any NP machine’s computation to a SAT formula. SAT remains a central problem: many other problems are proved NP-complete by reductions from SAT. A notable special case is **3-SAT**, where the formula is in CNF with exactly 3 literals per clause – 3-SAT is also NP-complete.

**Examples of NP-complete problems:** Besides SAT, classic NP-complete problems include: **Traveling Salesman (decision version)**, **3-SAT**, **Clique** (does a graph contain a clique of size ≥ k?), **Vertex Cover** (does a vertex cover of size ≤ k exist?), **Subset Sum/Partition**, **Hamiltonian Cycle**, **Graph Coloring**, etc. Each of these can be reduced to each other. The existence of so many diverse NP-complete problems indicates a deep connectivity – a solution to one gives a solution to all.

**Reductions:** To show a problem AA is NP-hard, we reduce a known NP-hard problem BB to AA. “Reduce” means transform instances of BB to instances of AA in polynomial time such that “yes” for AA corresponds to “yes” for BB. This is like saying: if we had a polynomial solver for AA, we could use it (via the reduction) to solve BB in polynomial time. For NP-completeness, one typically takes a known NP-complete problem and reduces it to the new problem in question. This is the standard technique to prove new problems NP-complete.

**Decision vs Optimization vs Search:** Many NP problems have related forms:

- **Decision problem:** asks a yes/no question (e.g., “Does there exist a solution of size ≤ k?”).
    
- **Optimization problem:** asks for the optimal value (e.g., “What is the minimum vertex cover size?” or “Find the maximum value achievable?”).
    
- **Search problem:** asks for the solution itself (e.g., “Find the actual set of vertices that is a minimum vertex cover.”).
    

For NP-completeness we typically frame problems as decision versions (yes/no) because NP is defined for decision problems. However, the optimization or search versions are often just as hard in practice. Reductions usually go through the decision version. For example:

- **Vertex Cover decision:** “Given GG and integer kk, does GG have a vertex cover of size ≤ k?”
    
- **Vertex Cover optimization:** “Find the minimum size of a vertex cover in GG.”
    
- **Vertex Cover search:** “Find one actual vertex cover of minimum size.”
    

Decision is in NP, and it’s NP-complete for Vertex Cover. The optimization and search versions are NP-hard (you could solve the decision by repeatedly solving the optimization or vice versa). Often, an efficient algorithm for the optimization version (finding the optimum or the optimal set) would yield an efficient decision solver too.

**Cook–Levin Theorem:** This theorem states that SAT is NP-complete. It was the first such result and essentially showed **NP ⊆ P(SAT)** (every NP problem can be reduced to SAT). The proof encodes an arbitrary nondeterministic polynomial-time Turing machine computation as a boolean formula (basically, a giant “exponential size” truth-table condensed by logic, or a tableau of the machine’s computation). This established NP-completeness and opened the door to proving other problems NP-complete by reductions. After SAT, Karp in 1972 gave 21 NP-complete problems (including Clique, Vertex Cover, Hamiltonian Cycle, Subset Sum, etc.), each by reducing from another NP-complete problem, creating a web of NP-complete problems.

To summarize:

- P = problems solvable in poly time.
    
- NP = problems verifiable in poly time (solutions guessed can be checked quickly). We know P ⊆ NP, but it’s open whether P = NP.
    
- NP-hard = at least as hard as any NP problem (solving it quickly would solve all NP problems quickly).
    
- NP-complete = in NP and NP-hard. These are the hardest problems in NP; if any one of them is in P, then P = NP.
    
- Many practical problems are NP-complete, meaning no known polynomial solution exists. To deal with them, we use heuristics, approximations, or special-case algorithms.
    

> **Practice Q1 (Complexity):**  
> a. What is the **Satisfiability (SAT)** problem?  
> b. What does it mean for a problem to be **NP-hard**?  
> c. What is an **NP-complete** problem?  
> d. State the **Cook–Levin Theorem**.

**Solution:**  
a. **SAT** is the Boolean Satisfiability Problem: given a boolean formula (usually in CNF form as a set of clauses ANDed together), determine if there exists an assignment of TRUE/FALSE values to its variables that makes the entire formula evaluate to TRUE. If such an assignment exists, the formula is “satisfiable.” If not, it’s unsatisfiable. SAT was the first problem proven NP-complete.  
b. **NP-hard** means “at least as hard as any NP problem.” Formally, a problem XX is NP-hard if every problem in NP can be **polynomial-time reduced** to XX. Intuitively, an NP-hard problem is one that could solve all NP problems if we had a polynomial algorithm for it. NP-hardness does _not_ require XX to be in NP (it might not even be decidable or might be an optimization problem).  
c. **NP-complete** describes problems that are both in NP and NP-hard. These are the “complete” problems of NP – the toughest problems in NP in the sense that a polynomial solution to one NP-complete problem implies polynomial solutions for all NP problems. Equivalently, YY is NP-complete if (i) Y∈NPY \in \text{NP}, and (ii) some known NP-complete problem reduces to YY (which, by transitivity, means every NP problem reduces to YY). If any NP-complete problem is shown to be in P, then P = NP.  
d. **Cook–Levin Theorem:** _SAT is NP-complete_. This foundational theorem (independently proven by Stephen Cook and Leonid Levin in 1971) established that any problem in NP can be transformed in polynomial time into an instance of SAT. In other words, SAT is at least as hard as any problem in NP. Since SAT is also in NP (a candidate assignment can be verified in polynomial time), SAT is NP-complete. The Cook–Levin theorem was the first step in identifying NP-complete problems and implies that a efficient (poly-time) algorithm for SAT would imply P=NPP = NP.

> **Practice Q2 (NP-Complete Example):** The **Vertex Cover** decision problem is: “Given an undirected graph GG and an integer kk, does GG have a vertex cover of size ≤ kk?” (A vertex cover is a set of vertices such that every edge has at least one endpoint in the set.)  
> a. Formulate the **decision**, **search**, and **optimization** versions of Vertex Cover.  
> b. Explain what it means that Vertex Cover is NP-complete.

**Solution:**  
a. For Vertex Cover:

- **Decision version:** “Does there exist a vertex cover of size ≤ kk in graph GG?” This expects a YES/NO answer given GG and kk.
    
- **Search version:** “Find a vertex cover of minimum size for graph GG” (or simply “find a vertex cover of size ≤ kk” if we consider the search corresponding to the decision problem when the answer is YES). This requires outputting the actual set of vertices (the cover) that solves the problem.
    
- **Optimization version:** “What is the minimum size of a vertex cover in GG?” This asks for the optimum value (a number). One could also phrase the optimization problem as “find a smallest vertex cover.”
    

These are interrelated: The optimization problem’s answer is the smallest kk for which the decision problem returns YES. The search problem asks for the actual set achieving that optimum.

b. Vertex Cover is NP-complete means two things: (1) It is in NP, and (2) it is NP-hard. Vertex Cover is in NP because given a set of vertices as a certificate, we can verify in polynomial time that it’s a cover by checking every edge – ensuring each edge touches one of the vertices in the set (that’s O(E)O(E) checks). Vertex Cover is NP-hard because there is a known polynomial-time reduction from a known NP-complete problem (for example, from 3-SAT or from Independent Set, etc.) to Vertex Cover. In fact, Vertex Cover was one of Karp’s 21 NP-complete problems, shown NP-complete by reduction from NP-complete **Clique** problem (Clique and Vertex Cover are complements). NP-complete implies that if we could solve Vertex Cover efficiently (in polynomial time), then we could solve all NP problems in polynomial time (i.e., NP ⊆ P). Conversely, since no one has found a polynomial algorithm for any NP-complete problem (including Vertex Cover) after decades of study, it’s strongly believed that no such algorithm exists (i.e., P≠NP, so we must use exponential-time algorithms, approximation, or heuristics for Vertex Cover in general).