### Combined Computer Science Notes

---

### Greedy Algorithms

- A **greedy algorithm** builds up a solution piece by piece, always choosing the option that looks the best at the moment.
    
- **Key property**: It never reconsiders choices; it assumes that by choosing local optimums, it reaches the global optimum.
    
- **Often recursive** and fast.
    
- Works well for certain optimization problems but doesn’t always give the best solution.
    
- **Example**: Huffman Coding — constructs an optimal prefix code based on character frequencies.
    

### Huffman Coding

- **Goal**: Efficient data compression.
    
- Assigns **shorter codes to more frequent characters**.
    
- Saves **20%–90%** in space depending on input distribution.
    
- Builds a binary tree where leaf nodes represent characters.
    
- Constructed using a **greedy algorithm** — combine least frequent elements iteratively.
    

### Coding Theory

- Studies how to detect and correct errors in data transmission.
    
- Includes **error-correcting codes** and **error-detecting codes**.
    
- **Human error** is the most frequent type; coding theory helps mitigate its effects.
    

---

### Graph Algorithms

#### Representations

- **Adjacency Matrix**: $O(V^2)$ space; good for dense graphs.
    
- **Adjacency List**: Efficient for sparse graphs.
    
- **Incidence Matrix**: Binary matrix; rows = vertices, columns = edges.
    
- **DIMACS format**: Standardized format used in competitions and algorithm benchmarks.
    

#### Search

- **BFS (Breadth-First Search)**:
    
    - Explores level by level.
        
    - Finds shortest paths in unweighted graphs.
        
    - May include **cross-edges** but not **back-edges**.
        
- **DFS (Depth-First Search)**:
    
    - Explores deeply first.
        
    - Can detect **cycles** via **back-edges**.
        
    - DFS tree doesn’t include cross-edges.
        

#### Topological Sort

- Applies to **DAGs (Directed Acyclic Graphs)**.
    
- Sorts vertices so for each edge $u \rightarrow v$, $u$ comes before $v$.
    
- Used in **task scheduling**, **build systems**, and **dependency resolution**.
    

#### Hypergraph

- A **hypergraph** allows edges (called **hyperedges**) to connect more than two vertices.
    
- Useful for modeling **multi-way relationships**, e.g., in database theory and VLSI design.
    

---

### Minimum Spanning Tree (MST)

- A **spanning tree** connects all vertices with **minimum total edge weight**.
    
- Used in network design, clustering, etc.
    
- **Prim’s Algorithm**:
    
    - Grows MST from a start vertex.
        
    - Selects the **smallest edge** connecting the tree to a new vertex.
        
- **Kruskal’s Algorithm**:
    
    - Sorts all edges by weight.
        
    - Adds the **next smallest edge** if it doesn’t form a cycle.
        
    - Both use Union-Find or priority queues; runtime: $O(E \log V)$.
        

---

### Single-Source Shortest Path

- **Goal**: Find shortest path from one vertex to all others.
    
- **Dijkstra’s Algorithm**: Efficient for graphs with **non-negative weights**.
    
- **Bellman-Ford Algorithm**: Handles graphs with **negative edge weights**.
    
- Used in routing protocols, maps, and AI navigation.
    

---

### Connectivity in Graphs

- **Matrix Powering**:
    
    - Repeated multiplication of the **adjacency matrix** finds reachability.
        
- **Floyd-Warshall Algorithm**:
    
    - Computes **all-pairs shortest paths**.
        
    - Dynamic programming algorithm.
        
    - Useful for dense graphs; runs in $O(V^3)$.
        

---

### Horner's Rule

- Efficient polynomial evaluation using nested multiplication.
    
- Example:
    
    - $ax^3 + bx^2 + cx + d$ becomes $(((a)x + b)x + c)x + d$.
        
- Reduces number of operations from $O(n^2)$ to $O(n)$.
    

---

### Network Flow

#### Flow Network Basics

- A **flow network** is a directed graph with capacities.
    
- Has a **source (s)** and **sink (t)**.
    
- Must obey:
    
    - **Capacity constraint**: $0 \leq f(u,v) \leq c(u,v)$
        
    - **Skew symmetry**: $f(u,v) = -f(v,u)$
        
    - **Flow conservation**: Sum of inflow = outflow at intermediate nodes.
        

#### Augmenting Paths

- Path from $s$ to $t$ where additional flow can be pushed.
    
- Use **residual graph** (remaining capacity).
    
- Flow is increased along the bottleneck (minimum capacity on the path).
    

#### Ford-Fulkerson Algorithm

1. Start with 0 flow.
    
2. While an augmenting path exists, augment flow.
    
3. Update residual graph.
    

- **Edmonds-Karp** version uses BFS: $O(VE^2)$.
    

#### Max-Flow Min-Cut Theorem

- Maximum flow from $s$ to $t$ equals the **minimum cut capacity** that separates $s$ and $t$.
    

---

### Applications of Network Flow

#### Maximum Bipartite Matching

- Convert bipartite graph to a flow network:
    
    - $s \rightarrow$ left set, right set $\rightarrow t$.
        
    - Edge capacity = 1.
        
    - Run max-flow: matching size = flow value.
        

#### Edge Connectivity

- Measures **minimum number of edges** to remove to disconnect a graph.
    
- Convert edges to two arcs with unit capacity.
    
- Run flow from one node to all others.
    

#### All-Pairs Connectivity

- Run flow between all pairs $(a, b)$.
    
- Helps compute global edge resilience of the network.
    

---

### Boolean Matrix Decidability

#### Problem

- Given row sums ${r_1, ..., r_m}$ and column sums ${c_1, ..., c_n}$:
    
    - Does a Boolean matrix exist such that each row has $r_i$ 1s and each column has $c_j$ 1s?
        

#### Flow-Based Solution

- Build bipartite graph (rows $\rightarrow$ columns).
    
- Add source $\rightarrow$ row nodes (capacity = $r_i$).
    
- Add column nodes $\rightarrow$ sink (capacity = $c_j$).
    
- Edges from rows to columns have capacity 1.
    
- If max-flow = total number of 1s, such a matrix exists.
    

---

### Linear Programming

#### Overview

- **Optimization technique** with **linear objective** and **linear constraints**.
    
- Examples: resource allocation, scheduling, and economics.
    

#### Forms

- **Standard Form**: Maximize $c^T x$ subject to $Ax \leq b$, $x \geq 0$
    
- **Slack Form**: Converts inequalities to equalities by adding **slack variables**.
    

#### Solutions

- **Feasible**: Satisfies all constraints.
    
- **Infeasible**: Violates at least one constraint.
    
- **Optimal**: Feasible with best objective value.
    

#### Simplex Algorithm

- Explores vertices of the feasible region.
    
- Moves to adjacent vertices with better objective value.
    
- Guaranteed to find the optimal solution at a corner.
    

#### Interior-Point Methods

- Navigate inside the feasible region.
    
- Asymptotically better for **large-scale LPs**.
    

---

### Polynomial Multiplication & FFT

#### Problem

- Multiply $A(x)$ and $B(x)$ (degree $\leq n$): naive time = $O(n^2)$.
    

#### Fast Fourier Transform (FFT)

- Evaluates polynomials at **roots of unity**.
    
- Uses **DFT**: Aj=∑k=0N−1ake−2πijk/NA_j = \sum_{k=0}^{N-1} a_k e^{-2\pi i jk/N}
    
- Inverse FFT recovers coefficients.
    
- Time: $O(n \log n)$.
    
- Leverages symmetry in complex numbers.
    

---

### Cryptology

#### One-Time Pad

- XOR message with a truly random key of same length.
    
- **Provably unbreakable**, but requires key to be used once.
    

#### Number Theory Foundations

- **Divisibility**: $m \mid n \Leftrightarrow n \equiv 0 \mod m$
    
- **Prime**: Has exactly two distinct positive divisors.
    
- **Unique Factorization Theorem**: Any $n > 1$ is a product of primes.
    
- **Infinitely many primes**: Proven via contradiction (Euclid).
    
- **Fermat’s Little Theorem**: $a^{p-1} \equiv 1 \mod p$ if $p$ is prime and $p \nmid a$
    

#### RSA Algorithm

1. Pick large primes $p$, $q$
    
2. $n = pq$, $\phi(n) = (p - 1)(q - 1)$
    
3. Choose $e$ such that $\gcd(e, \phi(n)) = 1$
    
4. Find $d$ such that $ed \equiv 1 \mod \phi(n)$
    
5. **Encrypt**: $C = M^e \mod n$
    
6. **Decrypt**: $M = C^d \mod n$
    

---

### Complexity Theory

#### Turing Machines

- Abstract machine model that formalizes computation.
    
- Can **accept**, **reject**, or **run forever**.
    

#### Language Classes

- **Recursive**: Machine always halts.
    
- **Recursively Enumerable (RE)**: Machine halts only on strings in the language.
    
- If both a language and its complement are RE, the language is recursive.
    

#### P vs. NP

- **P**: Problems solvable in polynomial time.
    
- **NP**: Problems verifiable in polynomial time.
    
- Unknown if $P = NP$.
    

#### NP-Hard / NP-Complete

- **NP-Hard**: At least as hard as the hardest problems in NP.
    
- **NP-Complete**: In NP and NP-Hard.
    
- Use **reductions** to show NP-completeness.
    

#### SAT (Boolean Satisfiability)

- First known NP-complete problem.
    
- **3-SAT**: Every clause has 3 literals; still NP-complete.
    
- Used in many complexity reductions.
    

#### Decision, Optimization, and Search

- **Decision**: Yes/No
    
- **Optimization**: Find best solution
    
- **Search**: Find one solution
    
- Often reductions exist between them.
    

---