### Greedy Algorithms
- Makes the best local choice at each step, aiming for global optimality.
- Often recursive and used in optimization problems.
- May not always give the best solution.
- **Example**: Huffman Coding (data compression).
### Huffman Coding
- Uses variable-length codes for characters.
- Compresses data efficiently (20%–90%).
- Builds a binary tree from character frequencies using a greedy algorithm.
### Coding Theory
- Focuses on detecting and correcting errors in communication.
- Human error is the most common source of errors.

---

### Graph Algorithms

#### Representations
- **Adjacency Matrix**: 2D array; good for dense graphs.
- **Adjacency List**: Efficient for sparse graphs.
- **Incidence Matrix**: Rows = vertices, Columns = edges.
- For large graphs, use **DIMACS format**.

#### Search
- **BFS**: Level-order traversal; finds shortest paths; allows cross-edges, no back-edges.
- **DFS**: Explores deeply first; allows back-edges (indicating cycles), no cross-edges.

#### Topological Sort

- Works on DAGs (Directed Acyclic Graphs).
    
- Orders nodes such that for every edge u → v, u comes before v.
    

#### Hypergraph

- A general graph where an edge (hyperedge) can connect more than two vertices.
    

---

### Minimum Spanning Tree (MST)

- Connects all vertices with the minimum total edge weight.
    
- **Prim’s**: Grows from a single node using the smallest edge.
    
- **Kruskal’s**: Adds smallest available edge without forming cycles.
    
- Both run in O(E log V).
    

---

### Single-Source Shortest Path

- Finds shortest path from one source to all other nodes.
    
- Algorithms: **Dijkstra's**, **Bellman-Ford**.
    

---

### Connectivity in Graphs

- **Matrix Powering**: Raises adjacency matrix to powers to determine connectivity.
    
- **Floyd-Warshall Algorithm**: Computes shortest paths between all pairs of nodes.
    

---

### Horner's Rule

- Efficient polynomial evaluation by factoring: `(((a)x + b)x + c)x + d`
    

---

### Network Flow

#### Flow Network Basics

- Directed graph with **capacities**.
    
- Special nodes: **Source (s)** and **Sink (t)**.
    
- Must obey flow conservation: flow in = flow out for intermediate nodes.
    

#### Flow Definitions

- Flow f(u,v) satisfies:
    
    - $0 \leq f(u,v)$ \leq capacity(u,v)
        
    - Skew symmetry: $f(u,v)$ = -f(v,u)
        
    - Flow conservation at all nodes except s and t.
        

#### Augmenting Paths

- Paths where more flow can be pushed.
    
- Residual capacity = capacity - current flow.
    

#### Ford-Fulkerson Algorithm

1. Initialize flow to 0.
    
2. Find augmenting paths using BFS/DFS.
    
3. Augment flow.
    
4. Repeat until no more paths.
    

- Runtime: O(VE^2) (Edmonds-Karp version).
    

#### Residual Graph

- Shows remaining capacity.
    
- Includes backward edges for reversing flow.
    

#### Max-Flow Min-Cut Theorem

- Max flow = capacity of the minimum s-t cut.
    

---

### Applications of Network Flow

#### Maximum Bipartite Matching

- Convert bipartite graph into flow network.
    
- Add source to left set, sink to right set.
    
- Match size = max flow.
    

#### Edge Connectivity

- Minimum edges needed to disconnect the graph.
    
- Convert undirected edges into directed arcs.
    
- Run max flow from one node to all others.
    

#### All-Pairs Connectivity

- Run max flow between all node pairs.
    
- Helps compute global edge connectivity.
    

---

### Boolean Matrix Decidability

#### Problem

- Given row sums {r1, ..., rm} and column sums {c1, ..., cn}, does a Boolean matrix exist that satisfies them?
    

#### Flow-Based Solution

1. Construct a bipartite graph: rows → columns.
    
2. Add source → row nodes (capacity = row sum).
    
3. Add column nodes → sink (capacity = column sum).
    
4. Internal edges (row → column) have capacity 1.
    

- Run max flow from source to sink.
    
- If flow = total number of 1s, such a matrix exists.
    

---

### Linear Programming

#### Overview

- Mathematical optimization with linear objective & constraints.
    
- Goal: maximize or minimize a function under linear constraints.
    

#### Forms

- **Standard Form**: Inequalities and non-negative variables.
    
- **Slack Form**: Adds variables to convert inequalities into equalities.
    

#### Solutions

- **Feasible**: Meets all constraints.
    
- **Optimal**: Best feasible solution.
    
- **Infeasible**: No solution satisfies all constraints.
    

#### Simplex Algorithm

- Starts at a corner of feasible region.
    
- Moves to adjacent corners for better objective value.
    
- Continues until no improvement.
    

#### Interior-Point Methods

- Move through interior of feasible region.
    
- Often faster for large problems.
    

---

### Polynomial Multiplication & FFT

#### Problem

- Multiply polynomials A(x) and B(x), each degree ≤ n.
    
- Direct multiplication = O(n^2).
    

#### Fast Solution

- Use the identity: y = g^{-1}(h(g(x)))
    
    - g = transform (FFT), h = point-wise multiply, g^{-1} = inverse FFT
        

#### FFT Strategy

1. Evaluate A and B at carefully chosen points (roots of unity).
    
2. Multiply corresponding values.
    
3. Apply inverse FFT.
    

- Time: O(n log n)
    

#### Why FFT Works

- Uses symmetry of complex roots of unity.
    
- Efficiently evaluates/interpolates polynomials.
    

---

### Cryptology

#### One-Time Pad

- XOR message with a random bitstream (pad).
    
- Provably secure but impractical due to key sharing.
    

#### Number Theory for Cryptography

- **Divisibility**: m divides n if n % m = 0.
    
- **Primes**: Only divisible by 1 and itself.
    
- **Unique Factorization**: Every integer > 1 = product of primes.
    
- **Infinitely many primes**: proved by contradiction.
    

#### Fermat’s Little Theorem

- If p is prime and a not divisible by p: $a^{p-1} \equiv 1 \ (mod\ p)$
    

#### RSA Algorithm

1. Choose two large primes p, q.
    
2. Compute n = p * q.
    
3. Compute totient $\phi(n)$ = (p-1)(q-1).
    
4. Choose public exponent e (gcd(e, $\phi(n)$) = 1).
    
5. Compute private key d such that $ed \equiv 1 \ (mod\ \phi(n)$).
    
6. Public key: (e, n), Private key: (d, n)
    
7. Encrypt: $C=Memod  nC = M^e \mod n$, Decrypt: $M=Cdmod  nM = C^d \mod n$
    

Security depends on difficulty of factoring large n.

---

### Complexity Theory

#### Turing Machines

- Abstract model of computation.
    
- Can accept, reject, or run forever.
    

#### Language Classes

- **Recursive**: Always halts with yes/no.
    
- **Recursively Enumerable (RE)**: Halts on strings in the language.
    
- A language is recursive ⟹ also RE.
    
- RE & co-RE ⟹ Recursive.
    

#### Deterministic vs. Nondeterministic

- Deterministic: One computation path.
    
- Nondeterministic: Multiple possible paths.
    

#### P vs. NP

- **P**: Problems solvable in polynomial time (deterministic).
    
- **NP**: Solutions verifiable in polynomial time.
    
- Open problem: Is P = NP?
    

#### NP-Hard & NP-Complete

- **NP-Hard**: At least as hard as any NP problem.
    
- **NP-Complete**: NP-Hard and in NP.
    

#### Boolean Satisfiability (SAT)

- Is there a variable assignment to make a Boolean formula true?
    
- First known NP-complete problem.
    
- Often represented in CNF.
    
- 3-SAT is also NP-complete.
    

---

### Decision, Optimization, and Search Problems

#### Forms

1. **Decision**: Yes/No question.
    
2. **Optimization**: Maximize/minimize objective.
    
3. **Search**: Find an actual solution.
    

#### Examples

- **SAT**: Find a satisfying assignment (search), or just check if one exists (decision).
    
- **Longest Path**: Is there a path of length ≥ k? What’s the longest?
    
- **Vertex Cover**: Does one exist of size ≤ k? Find it. What’s the smallest?
    

These forms are interrelated but have different complexities.