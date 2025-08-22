# Computer Science 581 Exam 2: Comprehensive Study Guide

This study guide is intended to teach and prepare you for the upcoming CS 581 Exam 2. It is based on three previous years' exams and detailed personal notes. It assumes no prior in-depth preparation and is written to help you build a strong conceptual and practical understanding of each topic from the ground up.

---

## 1. Greedy Algorithms

### What Are Greedy Algorithms?

Greedy algorithms are a type of algorithmic strategy used to solve optimization problems. The core idea is to build up a solution step-by-step, always choosing the option that looks best at the moment. This local optimum is hoped to lead to a global optimum.

Unlike other methods such as dynamic programming or backtracking, greedy algorithms do not revisit or revise earlier choices.

### When Do Greedy Algorithms Work?

Greedy algorithms only work for a specific class of problems where a local optimum choice at each stage leads to the overall optimal solution. These are problems that exhibit the **greedy-choice property** and **optimal substructure**.

### Example: Huffman Coding

**Purpose**: Used for lossless data compression. The goal is to assign shorter binary codes to more frequent characters.

**Steps:**

1. **Frequency Analysis**: Count frequency of each character.
    
2. **Build Priority Queue**: Insert each character as a node with frequency as key.
    
3. **Build Tree**:
    
    - Remove two nodes with lowest frequency.
        
    - Combine them into a new node with frequency equal to the sum.
        
    - Reinsert this new node into the queue.
        
    - Repeat until one node remains (root of Huffman Tree).
        
4. **Assign Codes**: Traverse the tree from root to leaves:
    
    - Left edge = 0
        
    - Right edge = 1
        

**Properties:**

- Prefix-free: No code is a prefix of another.
    
- Guaranteed to be optimal for given frequency distribution.
    

**Exam Example:** Design a Huffman code for a file with character frequencies: a:57, b:88, c:25, d:71, e:63, f:39

---

## 2. Network Flow and Boolean Matrix Construction

### What Is Network Flow?

A **flow network** is a directed graph where each edge has a capacity, and each edge receives a flow. It models systems like data traffic, pipelines, or job assignments.

**Terminology:**

- **Source (s)**: Where flow originates.
    
- **Sink (t)**: Where flow terminates.
    
- **Capacity constraint**: Flow on edge (u,v) cannot exceed its capacity.
    
- **Skew symmetry**: f(u,v) = -f(v,u)
    
- **Flow conservation**: At any node except s and t, total inflow = total outflow.
    

### Ford-Fulkerson Algorithm

This algorithm computes the **maximum flow** in a network.

**Steps:**

1. Initialize all flows to 0.
    
2. While there is an **augmenting path** from s to t in the **residual graph**, do:
    
    - Find path from s to t where capacity > 0.
        
    - Compute the **bottleneck capacity** (min capacity along the path).
        
    - Add flow to each edge in the path and subtract from reverse edges.
        
3. Repeat until no augmenting path exists.
    

**Edmonds-Karp Variant:**

- Uses BFS to find shortest augmenting paths.
    
- Time complexity: O(VE^2)
    

### Boolean Matrix Decidability

**Problem:** Given a matrix of size m x n with target row sums and column sums, does a matrix of 0s and 1s exist that satisfies these?

**Solution Using Flow:**

1. Model as a bipartite graph:
    
    - Left: row nodes
        
    - Right: column nodes
        
    - Add edges from rows to columns with capacity = 1
        
2. Add source node with edges to each row node (capacity = target row sum)
    
3. Add sink node with edges from column nodes (capacity = target col sum)
    
4. Run max-flow from source to sink
    
5. If max flow = total number of 1s (sum of row sums), then a valid matrix exists.
    

**Example:** Row sums: (2,2,3,3,4) Column sums: (1,2,3,4,4) Resulting Boolean matrix from previous exam:

```
1 0 1 0 0
0 0 0 1 1
0 0 1 1 1
0 1 0 1 1
0 1 1 1 1
```

---

## 3. Linear Programming

### What Is Linear Programming?

Linear programming (LP) is a method to achieve the best outcome (maximum or minimum) of a linear objective function, subject to linear constraints (equalities/inequalities).

**Standard Form:**

- Maximize: c^T x
    
- Subject to: Ax <= b
    
- x >= 0
    

**Slack Form:**

- Converts all inequalities to equalities by introducing **slack variables**.
    

### Simplex Algorithm

An iterative procedure for solving LP problems.

**Steps:**

1. Convert the problem into **slack form**.
    
2. Select an **entering variable** with a positive coefficient in the objective function.
    
3. Determine the **leaving variable** based on the smallest ratio of constraint RHS to the coefficient of the entering variable.
    
4. **Pivot**: Replace leaving variable with entering one in the equations.
    
5. Update all equations and repeat until no more improvements.
    

**Properties:**

- Operates on the vertices of the feasible region.
    
- Guaranteed to find the optimal solution if it exists.
    

**Example:** Maximize: 3x1 + x2  
Subject to:

- 4x1 + x2 <= 7
    
- x1 + x2 <= 5
    
- x1, x2 >= 0
    

---

## 4. Fast Fourier Transform (FFT)

### What Problem Does FFT Solve?

Naively multiplying two polynomials of degree n takes O(n^2) time. FFT enables this in O(n log n).

### How It Works

1. **Polynomial Evaluation:** Represent polynomials as functions and evaluate at roots of unity.
    
2. **Pointwise Multiplication:** Multiply corresponding values of two evaluated polynomials.
    
3. **Interpolation:** Apply inverse FFT to recover the resulting polynomial.
    

### Key Insight: Symmetry

The FFT uses **roots of unity** and their symmetry:

- Split A(x) into even (A_e) and odd (A_o) parts: A(x) = A_e(x^2) + xA_o(x^2)
    
- This reduces evaluations from n points to n/2 recursively.
    

**Time Complexity:** O(n log n)

---

## 5. Cryptography (RSA)

### Foundations in Number Theory

- **Fermat’s Little Theorem**: If p is prime and a not divisible by p, then a^(p-1) ≡ 1 (mod p)
    
- **GCD**: Greatest common divisor. Used to check if numbers are coprime.
    

### RSA Algorithm

1. Choose two distinct large primes p, q
    
2. Compute n = pq, and phi(n) = (p-1)(q-1)
    
3. Choose public exponent e such that gcd(e, phi(n)) = 1
    
4. Compute private exponent d such that ed ≡ 1 mod phi(n)
    
5. Public key = (n, e), Private key = (n, d)
    
6. Encrypt: C = M^e mod n
    
7. Decrypt: M = C^d mod n
    

**Example (from exam):**

- p = 7, q = 13 → n = 91
    
- phi(91) = (7-1)(13-1) = 72
    
- e = 5, find d: 5d ≡ 1 mod 72 → d = 29
    

Encrypt:

- M = 3 → C = 3^5 mod 91 = 243 mod 91 = 61
    

---

## 6. Complexity Theory

### Key Problems

- **Vertex Cover**: Choose minimum set of vertices such that every edge is incident to at least one vertex in the set.
    

### Problem Variants

- **Decision**: Does there exist a vertex cover of size ≤ k?
    
- **Search**: Find such a vertex cover.
    
- **Optimization**: Find the smallest vertex cover.
    

### Complexity Classes

- **P**: Problems solvable in polynomial time.
    
- **NP**: Problems verifiable in polynomial time.
    
- **NP-Complete**: Problems in NP and as hard as any problem in NP.
    
- **NP-Hard**: At least as hard as NP-Complete, may not be in NP.
    

### Cook-Levin Theorem

Proves that the Boolean satisfiability problem (SAT) is NP-complete. It was the first problem to be shown NP-complete, forming the basis of NP-completeness theory.

### SAT Problem

Given a Boolean formula, is there an assignment of variables that makes it true?

---

## 7. Supplementary Topics

### Dynamic Programming

Solves problems by breaking them into overlapping subproblems.

Time to solve an n-stage decision process with d decisions per stage is O(nd).

### Graph Search

- **BFS**: Finds shortest path in unweighted graphs; explores level by level.
    
- **DFS**: Detects cycles using back edges; explores deeply.
    

**Topological Sort**:

- Applies to DAGs (Directed Acyclic Graphs)
    
- Sorts nodes so that for each edge u → v, u appears before v
    

### Graph Representations

- **Adjacency Matrix**: O(V^2), efficient for dense graphs
    
- **Adjacency List**: O(V+E), efficient for sparse graphs
    

---

This concludes the comprehensive guide. Make sure to understand each section deeply and refer back to examples from previous exams for reinforcement. Let me know if you'd like practice problems or visual diagrams added to this document.