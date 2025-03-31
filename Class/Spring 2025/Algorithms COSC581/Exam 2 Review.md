### **Greedy Algorithms**
- **Definition**: An algorithmic paradigm that makes the locally optimal choice at each step with the hope of finding the global optimum.
- **Nature**:
    - Often **recursive** in design.
    - Effective for **optimization problems**.
    - Not guaranteed to provide the best solution in all cases but works well for certain problems.
- **Key Use Case**: Huffman Coding.

---

### **Huffman Codes**
- **Purpose**: Data compression technique using variable-length codes for different characters.
- **Compression Efficiency**:
    - Saves **20% to 90%** in space, depending on the frequency distribution of input data.
- **Algorithmic Approach**:
    - Uses a **greedy algorithm** to construct the code tree.
    - Builds the **Huffman tree from the bottom up**, starting with the least frequent characters.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcq9taKYm5fSpzVl2YOAI7M24OwPxZD7kyb0-nKGBHtp2aTVL8_PvFZ2bHE-DD8HbU9bBZFS2xMTdoiKu5j6w23UiFa_ROlgx_ct6MyytjqzTvV8XF2kIpTbvlqrECFksGSNhIY_g?key=TeciyFeZkxkinNHwAGspCOdl)

---

### **Coding Theory**

- **Human Error**:
    - Most common source of errors in coding and communication systems.
    - Emphasis on designing codes to **detect and correct** errors caused by human mistakes.

---

### **Graph Algorithms**
- **Graph Representation**:
    - **Adjacency Matrix**: 2D matrix indicating direct connections between vertices.
    - **Adjacency List**: List where each vertex points to a list of connected vertices.
    - **Incident Matrix**:
        - Binary matrix.
        - **Rows** represent **vertices**.
        - **Columns** represent **edges**.
- **Graph Formats**:
    - Avoid adjacency matrix for **sparse or large graphs**.
    - Use **DIMACS format** for input/output in standardized graph algorithm problems.

---

### **Graph Searching**

#### **Breadth-First Search (BFS)**
- Explores graph level by level.
- **Finds shortest paths** in unweighted graphs.
- **Traversal order**: left to right or level-wise.
- **Edge types**:
    - Can include **cross-edges** (link different branches).
    - Cannot include **back-edges** (edges pointing back to ancestors).
#### **Depth-First Search (DFS)**
- Explores as deep as possible before backtracking.
- **Traversal order**: dives into one branch fully before moving to another.
- **Edge types**:
    - Allows **back-edges** → indicate **cycles**.
    - No **cross-edges** in DFS tree.

---

### **Topological Sort**
- **Graph Type**: Works on **Directed Acyclic Graphs (DAGs)**.
- **Goal**: Linearly order vertices such that for every directed edge `u → v`, vertex `u` comes before `v`.
- **Edge Terminology**: Directed edges are also known as **arcs**.
- **Visualization**:
    - Vertices arranged along the x-axis to represent flow.
- **Use Case**: Task scheduling, dependency resolution.

---

### **Hypergraph**
- Generalization of a graph.
- **Edges (hyperedges)** can connect **more than two vertices**.
- Used for higher-fidelity modeling in complex systems.

---

### **Minimum Spanning Trees (MST)**
- **Definition**: A subset of edges connecting all vertices in a weighted, undirected graph with minimum total edge weight.
- **If not all vertices are connected**, it’s a **forest**.
- **Algorithms**:
    - **Kruskal’s Algorithm**:
        - Sorts all edges.
        - Adds the **smallest weight edge** that doesn’t create a cycle.
        - Time complexity: **O(E log V)**.
    - **Prim’s Algorithm**:
        - Starts from a vertex and grows the MST by adding the **cheapest edge** connecting the tree to a new vertex.
        - Skips edges that would form cycles.
        - Also **O(E log V)** using priority queues.
- **Bandwidth**: Refers to the **longest edge** in the path — often minimized in MST variants.

---

### **Single-Source Shortest Path**
- **Objective**: Find the shortest path from a given source vertex to all other vertices.
- Common algorithms include **Dijkstra's** and **Bellman-Ford**.
- Measures **time or cost** to reach each node from the source.

---

### **Connectivity in Graphs**

- **Matrix Powering**:
    - Raise the **adjacency matrix** to powers to find connectivity (i.e., paths of certain lengths).
- **Warshall’s Algorithm / Floyd-Warshall Algorithm**:
    - Solves **transitive closure** (reachability) and **all-pairs shortest paths**.
    - Dynamic programming-based approach.
    - Efficient for dense graphs.


This just means: can you get from one node (vertex) in a graph to another?

Imagine a map of cities (nodes), and roads (edges) connecting them. **Connectivity** asks: is there **a route** between two cities?

---

#### 🧮 **Matrix Powering**

Every graph can be represented by an **adjacency matrix**.  
This is just a grid (matrix) where:

- Each row/column represents a node.
- A `1` means there’s a direct edge (connection) between the nodes.
- A `0` means no direct connection.

**Example:**

```
A -- B
|
C

Adjacency matrix:
   A B C
A [0 1 1]
B [1 0 0]
C [1 0 0]

```

Now here's the trick:
- If you **raise** this matrix to a power, like A2A^2A2, you get info about paths of **length 2**.
- A3A^3A3 gives info about paths of **length 3**, and so on.

So, **matrix powering helps find if paths of a certain length exist** between nodes.

---

#### ⚡ **Warshall’s Algorithm / Floyd-Warshall Algorithm**

Let’s split these:

##### ✅ Warshall's Algorithm

- Solves **transitive closure**:  
    Can you **reach** one node from another, ignoring path length?
    
- It updates the matrix so that if you can go from A to B, and B to C, it marks that A can go to C too.
    

> It's like checking all possible "friend of a friend" connections.

##### 🛣️ Floyd-Warshall Algorithm

- Does a bit more: it finds the **shortest paths between all pairs of nodes**.
    
- Still works with matrices.
    
- Uses **dynamic programming** (breaking down the problem into smaller subproblems and solving them efficiently).
    

> Best when you have a **dense graph** (many edges), because it looks at all possible connections.

---

#### 📋 Summary

| Concept              | What it does                                   | Useful for…              |
| -------------------- | ---------------------------------------------- | ------------------------ |
| Matrix Powering      | Finds if paths of certain lengths exist        | Connectivity over steps  |
| Warshall’s Algorithm | Finds if you can reach any node from any other | General reachability     |
| Floyd-Warshall       | Finds shortest paths between all pairs         | All-pairs shortest paths |

---

### **Horner's Rule**
- **Purpose**: Efficient polynomial evaluation.
- **Method**: Parentheses are added strategically to reduce the number of operations.
- **Example**:
    - Instead of computing:  
        `ax^3 + bx^2 + cx + d`
    - Horner’s form:  
        `(((a)x + b)x + c)x + d`

### **Network Flow**

---

### **1. Flow Network Basics**
- A **flow network** is a **directed graph (digraph)** with non-negative arc weights representing **capacities** (i.e., upper bounds on flow).
- It includes two **special vertices**:
    - **Source (s)**: Usually has **in-degree 0**; it is the origin of flow.
    - **Sink (t)**: Usually has **out-degree 0**; it is the destination for flow.
- A graph is only a flow network if:
    - It has exactly one **source** and one **sink**.
    - **Flow conservation** holds:
        - Total flow out of **source** = total flow into **sink**.
        - All **intermediate nodes** must have equal incoming and outgoing flow.

---

### **2. Flow Definitions**
- A **flow** is a function f(u,v)f(u, v)f(u,v) assigning a real number (flow value) to each arc such that:
    - **Capacity constraint**: f(u,v)≤c(u,v)f(u, v) \leq c(u, v)f(u,v)≤c(u,v)
    - **Skew symmetry**: f(u,v)=−f(v,u)f(u, v) = -f(v, u)f(u,v)=−f(v,u)
    - **Flow conservation**: For all u≠s,tu \not= s, tu=s,t:
        ∑vf(u,v)=0\sum_{v} f(u, v) = 0v∑​f(u,v)=0
        (i.e., inflow = outflow for all intermediate vertices)
        
- The **value of a flow** is the **net flow into the sink** (or net out of the source), which remains constant during flow operations.

---

### **3. Augmenting Paths**
- A **path from s to t** along which additional flow can be added.
- Conditions:
    - Each edge along the path has **residual capacity** (i.e., not full).
    - Residual capacity = capacity − current flow.
- **Augmentation**:
    - Find a path from **s to t** in the **residual graph**.
    - Determine the **minimum residual capacity** on that path (called the **bottleneck**).
    - **Increase the flow** along that path by the bottleneck value.
- If augmenting paths exist, the system is **not yet stable** (can still increase flow).

---

### **4. Ford-Fulkerson Algorithm**

#### **Goal**: Find the **maximum flow** from s to t.

**Procedure**:
1. **Initialize** all flows to zero.
2. While an **augmenting path** exists:
    - Use a **search algorithm** (e.g., DFS or BFS) to find a path in the residual graph.
    - Identify the **minimum residual capacity** along that path.
    - **Augment** the flow along the path.
    - Update the **residual graph**, including adding **backward edges** to allow reversal of previous flow.
3. **Repeat** until no augmenting path exists.

**Properties**:
- **Flow conservation** is maintained at each step.
- Algorithm terminates when **no augmenting paths remain**.
- Runtime depends on path selection:
    - If using **BFS** for shortest augmenting path, we get the **Edmonds-Karp algorithm**, which runs in:
        O(VE2)O(VE^2)O(VE2)

---

### **5. Residual Graph**
- A graph showing **available capacities** for further augmentation.
- Includes:
    - **Forward edges**: capacity = original capacity − current flow.
    - **Backward edges**: capacity = current flow (to allow undoing flow).
        
- Used to find **augmenting paths** in the Ford-Fulkerson process.

---

### **6. Max-Flow Min-Cut Theorem**

- States that the **maximum flow** from sss to ttt is equal to the **minimum capacity** of a **cut** that separates sss from ttt.
- A **cut** is a partition of vertices into two disjoint sets:
    - One containing sss, and the other containing ttt.
- The **capacity of the cut** is the sum of the capacities of edges going from the source side to the sink side.
- **Visual metaphor**: A vertical slicing plane that disconnects sss from ttt.
- This theorem guarantees **optimality** of Ford-Fulkerson's result.

---

### **7. Applications of Network Flow**

---

#### **7.1 Maximum Bipartite Matching**
- **Bipartite Graph**:
    - Two disjoint sets UUU and VVV.
    - Edges only go between UUU and VVV, not within.
- **Goal**: Find the **largest matching** — set of edges with no shared vertices.
    

**Steps Using Flow Network**:
1. Start with an undirected bipartite graph.
2. Add a **source sss**, connect it to each node in set UUU.
3. Add a **sink ttt**, and connect each node in set VVV to it.
4. Replace undirected edges (u,v)(u, v)(u,v) with **directed arcs u→vu \rightarrow vu→v**.
5. Set **capacity = 1** for all arcs.
6. Run **Ford-Fulkerson** to compute max flow.
7. The value of the flow = **maximum matching size**.

- **Min-Cut Theorem** ensures the matching found is optimal.

---

#### **7.2 Edge Connectivity**

- **Edge Connectivity**: The minimum number of edges that must be removed to **disconnect** the graph.

**Flow-Based Approach**:
1. Convert the undirected graph to a directed graph:
    - Each edge becomes **two directed arcs** (one in each direction), each with **capacity = 1**.
2. Choose an arbitrary node as **source (s)**.
3. For **every other node ttt** in the graph:
    - Compute the **maximum flow from sss to ttt**.
4. The **minimum of all max flows** found = the **edge connectivity** of the graph.

**Notes**:
- You don’t have to try every pair of (s,t)(s, t)(s,t).
    - It’s sufficient to **fix one node as sss** and try all others as ttt, due to symmetry.

---

#### **7.3 All-Pairs Connectivity via Max Flow**

- Goal: Measure **connectivity between every pair** of vertices.

**Procedure**:

1. Convert graph to a **flow network** with **unit capacities**.
2. For **every pair (a,b)(a, b)(a,b)**:
    - Treat aaa as source, bbb as sink.
    - Compute the **maximum flow** from aaa to bbb.
3. Record the minimum flow among all such pairs — this gives **global connectivity**.
4. **Important constraint**: You can **reuse vertices**, but not **reuse edges** for the same flow.


### Boolean Matrix Decidability

---

### What’s the Problem?

You’re given:
- A list of **row sums**: {r1,r2,...,rm}\{r_1, r_2, ..., r_m\}{r1​,r2​,...,rm​}
- A list of **column sums**: {c1,c2,...,cn}\{c_1, c_2, ..., c_n\}{c1​,c2​,...,cn​}
- Where:
    ∑ri=∑cj\sum r_i = \sum c_j∑ri​=∑cj​

**Goal**: Decide if there's a Boolean matrix (only 0s and 1s) of size m×nm \times nm×n such that:
- Each row iii has exactly rir_iri​ ones.
- Each column jjj has exactly cjc_jcj​ ones.

---

### Turning It Into a Flow Problem

We reduce the problem to a **maximum flow** problem using a flow network.

#### Step-by-Step:

1. **Create a Bipartite Graph**:
    - Left side: one node for each row R1,R2,...,RmR_1, R_2, ..., R_mR1​,R2​,...,Rm​
    - Right side: one node for each column C1,C2,...,CnC_1, C_2, ..., C_nC1​,C2​,...,Cn​
    - Connect each row to every column (complete bipartite graph)
        
2. **Add Source and Sink**:
    - Add a **source node** sss
        - Connect s→Ris \rightarrow R_is→Ri​ with capacity rir_iri​
    - Add a **sink node** ttt
        - Connect Cj→tC_j \rightarrow tCj​→t with capacity cjc_jcj​
3. **Connect Rows to Columns**:
    - For every possible matrix cell (i,j)(i, j)(i,j), add an edge:
        - Ri→CjR_i \rightarrow C_jRi​→Cj​ with **capacity 1**

---

### Running the Max Flow Algorithm

- Use any **max-flow algorithm** (like Ford-Fulkerson or Edmonds-Karp)
- Calculate the **maximum flow from sss to ttt**

---

### Decision Rule

- If the **max flow equals** the total number of ones (i.e., ∑ri\sum r_i∑ri​), then:
    - ✅ **Yes**, the Boolean matrix **exists**
- Otherwise:
    - ❌ **No**, such a matrix **does not exist**
        

---

### Why It Works

- Flow from RiR_iRi​ to CjC_jCj​ means a 1 is placed in position (i,j)(i, j)(i,j)
- Row sums are enforced by the capacity from sss to rows
- Column sums are enforced by the capacity from columns to ttt
- Capacity 1 ensures only 0 or 1 can go through a cell — matching Boolean values
    

---

### Example

Row sums: {2,1}\{2, 1\}{2,1}  
Column sums: {1,1,1}\{1, 1, 1\}{1,1,1}

1. Connect source to row1 (cap 2), row2 (cap 1)
2. Connect each row to all 3 columns (cap 1)
3. Connect columns to sink (each cap 1)
    

If the max flow is 3, the matrix exists.

### Linear Programming

---

### What is Linear Programming?

- **"Programming"** here is an old term that means **"planning"** or **"solving by tabulation."**
    
- A type of **Mathematical Optimization** that deals with:
    
    - **Numerical (not categorical)** variables
        
    - Finding the **best outcome** (max or min) under a set of constraints
        

---

### Types of Mathematical Programming

- **Linear Programming (LP)** – all relationships are linear
    
- **Quadratic Programming** – involves squared terms
    
- **Nonlinear Programming** – nonlinear relationships
    
- **Dynamic Programming** – solves problems by breaking them down recursively
    

---

### General LP Framework

Every LP problem consists of:

1. **Variables**: x1,x2,…,xnx_1, x_2, \ldots, x_nx1​,x2​,…,xn​
    
2. **Objective Function**:
    
    - A linear function to **maximize** or **minimize**  
        Example: Maximize 3x1+5x23x_1 + 5x_23x1​+5x2​
        
3. **Constraints**:
    
    - Restrictions on variable values, written as **linear inequalities or equalities**  
        Example:  
        x1+x2≤5x_1 + x_2 \leq 5x1​+x2​≤5  
        x1≥0,x2≥0x_1 \geq 0, x_2 \geq 0x1​≥0,x2​≥0
        

> All relationships in LP must be **linear** — no squares, products, logs, etc.

---

### Standard Form vs. Slack Form

#### Standard Form:

- All constraints are **“≤”** inequalities.
    
- Objective is to **maximize**.
    
- All variables ≥0\geq 0≥0.
    

#### Slack Form:

- Inequalities are turned into **equalities** by adding **slack variables**.
    
- Example:
    
    x1+x2≤5⇒x1+x2+s1=5x_1 + x_2 \leq 5 \quad \Rightarrow \quad x_1 + x_2 + s_1 = 5x1​+x2​≤5⇒x1​+x2​+s1​=5
    - s1s_1s1​ is a **slack variable** representing unused space.
        

#### Terms:

- **Basic variables**: Start on the **left** of the equations (e.g., slack variables).
    
- **Non-basic variables**: On the **right**; initially set to **0**.
    

---

### Types of Solutions

- **Feasible Solution**: Satisfies **all constraints**.
    
- **Infeasible Solution**: Violates **at least one constraint**.
    
- **Optimal Solution**: A feasible solution with the **best objective value** (max or min).
    

---

### Visualizing LP in 2D (Simplex Geometry)

- Constraints form **cutting planes** that define a **feasible region** (a polygon or polyhedron).
    
- In 2D, this region looks like a **shaded polygon**.
    
- The **Simplex Algorithm** explores **corners (vertices)** of this region.
    

---

### The Simplex Algorithm

- A popular method for solving LP problems.
    
- Works by:
    
    1. Starting at a **corner point** of the feasible region.
        
    2. Checking **adjacent corners** to see if the objective improves.
        
    3. **Moving** to a better corner until none improve.
        
- Guarantees the optimum is at one of the **vertices**.
    
- **Usually fast in practice**, even though there are rare worst-case examples where it's slow.
    

---

### Why the Simplex Works

- The feasible region (solution space) is a **convex polytope**.
    
- The **optimum** of a linear function over a convex shape lies at one of the **vertices**.
    
- Simplex moves from one vertex to another, improving the objective each time.
    

---

### Pivoting in Simplex

- **Pivot step**: Choose a non-basic variable (currently zero) to **increase**.
    
- Increase until it hits a constraint (becomes "tight").
    
- One basic variable will become non-basic (swap roles).
    
- Repeat until no improvement possible.
    

---

### Interior-Point Methods

- An alternative to Simplex, especially good for **very large problems**.
    
- Works by moving **inside** the feasible region rather than along its edges.
    
- Often **faster than Simplex** in high-dimensional cases.
    
- Not used as often in small/medium LP problems.
    

---

### Integer Linear Programming (ILP)

- When variables must take **integer values**.
    
- Much harder — **NP-complete**.
    
- You lose the ability to use techniques like Simplex directly.
    
- LP is "easy", but ILP is **computationally expensive**.
    

---

### Summary

|Concept|Meaning|
|---|---|
|Objective Function|The function you want to maximize or minimize|
|Constraints|Rules the solution must follow|
|Feasible Region|Set of all solutions that satisfy constraints|
|Slack Variable|Added to turn inequalities into equalities|
|Basic Variable|Initially has a value (like slack)|
|Non-Basic Variable|Starts at 0, used in pivoting|
|Simplex Algorithm|Moves from corner to corner to find optimum|
|Interior Point Method|Alternative that moves through interior|
### Polynomial Multiplication and the Fast Fourier Transform (FFT)

---

### The Problem

You’re given two polynomials:

- A(x)A(x)A(x) and B(x)B(x)B(x), each of degree ≤ nnn
    
- Goal: Compute C(x)=A(x)⋅B(x)C(x) = A(x) \cdot B(x)C(x)=A(x)⋅B(x)
    
    - C(x)C(x)C(x) will have **degree ≤ 2n**
        

---

### Direct Polynomial Multiplication

- Multiply term by term:  
    Each term in AAA gets multiplied by each term in BBB
    
- Time complexity:
    
    O(n2)O(n^2)O(n2)

---

### Can We Do Better?

Yes — **using the idea of transforming the problem**, just like in classic CS tricks.

### Transform-Based Strategy

We use a general idea:

- Compute y=f(x)y = f(x)y=f(x)
    
- Instead of computing fff directly, we use:
    
    y=g−1(h(g(x)))y = g^{-1}(h(g(x)))y=g−1(h(g(x)))
- Where:
    
    - ggg = **transform**
        
    - hhh = do something easier in transformed space
        
    - g−1g^{-1}g−1 = **inverse transform**
        

**Classic CS Example** (for context):  
Add two decimal numbers stored in “zoned decimal” format.

- ggg: convert to binary
    
- hhh: add
    
- g−1g^{-1}g−1: convert back to decimal
    

---

### Applying This to Polynomials

Let’s define a strategy:

1. **Transform both polynomials into point-value form**: evaluate them at some points
    
2. **Multiply the evaluations point-by-point**
    
3. **Use inverse transform to get back to coefficients**
    

---

### Polynomial Evaluation

- A polynomial of degree ddd is fully determined by its values at **d + 1 points**
    
- So to multiply A(x)A(x)A(x) and B(x)B(x)B(x) (degree ≤ nnn), we evaluate both at **2n+12n + 12n+1** distinct points
    

#### Direct Evaluation and Interpolation

- Evaluation = plugging values in: takes O(n)O(n)O(n) per point → O(n2)O(n^2)O(n2) total
    
- Interpolation = converting back from point-values to coefficients → also O(n2)O(n^2)O(n2)
    

> So, **direct evaluation + interpolation is no faster** than multiplying the coefficients.

---

### The Secret: Carefully Chosen Points

- What if we **pick the points** cleverly to take advantage of symmetry?
    
- This leads to the **Discrete Fourier Transform (DFT)** and **Fast Fourier Transform (FFT)**
    

---

### The FFT and DFT

#### What is the DFT?

Given:

- A list of values: a0,a1,...,aN−1a_0, a_1, ..., a_{N-1}a0​,a1​,...,aN−1​
    

The DFT produces:

Aj=∑k=0N−1ak⋅e−2πijk/NA_j = \sum_{k=0}^{N-1} a_k \cdot e^{-2\pi i jk / N}Aj​=k=0∑N−1​ak​⋅e−2πijk/N

- Think of this as evaluating a polynomial at NNN special points on the **complex unit circle**
    
- Those points are:  
    ω0,ω1,ω2,...,ωN−1\omega^0, \omega^1, \omega^2, ..., \omega^{N-1}ω0,ω1,ω2,...,ωN−1, where  
    ω=e2πi/N\omega = e^{2\pi i / N}ω=e2πi/N is a **primitive Nth root of unity**
    

#### Why It Helps

- The trick: those roots of unity have **algebraic symmetry**.
    
- Using them lets us evaluate (and interpolate) in **O(Nlog⁡N)O(N \log N)O(NlogN)** time via the **FFT**.
    

---

### Key Observations

- **DFT = evaluate polynomial at complex roots of unity**
    
- **Inverse DFT = interpolate from those values**
    
- If NNN is a power of 2, we can:
    
    - **Divide** the polynomial into even and odd terms
        
    - **Recursively apply FFT**
        
    - Combine results using symmetry:
        
        T(N)=2T(N/2)+O(N)⇒T(N)=O(Nlog⁡N)T(N) = 2T(N/2) + O(N) \Rightarrow T(N) = O(N \log N)T(N)=2T(N/2)+O(N)⇒T(N)=O(NlogN)

---

### Intuition Behind FFT

Let’s say:

a(x)=a0+a1x+a2x2+⋯+aN−1xN−1a(x) = a_0 + a_1x + a_2x^2 + \cdots + a_{N-1}x^{N-1}a(x)=a0​+a1​x+a2​x2+⋯+aN−1​xN−1

- Instead of plugging in arbitrary values of xxx, we plug in complex roots of unity:
    
    x=ωj=e2πij/Nx = \omega^j = e^{2\pi i j / N}x=ωj=e2πij/N
- Thanks to properties like:
    
    ωj+N/2=−ωj\omega^{j+N/2} = -\omega^jωj+N/2=−ωj
    
    we can **regroup terms**, **cancel nicely**, and compute recursively.
    

---

### Final Takeaways

- **Polynomial multiplication** becomes:
    
    1. Use FFT to evaluate AAA and BBB
        
    2. Multiply the evaluations (component-wise)
        
    3. Use inverse FFT to get coefficients of CCC
        
- **Time Complexity**:
    
    O(Nlog⁡N)(instead of O(N2))O(N \log N) \quad \text{(instead of } O(N^2) \text{)}O(NlogN)(instead of O(N2))
- **Fine print**:
    
    - FFT uses **complex numbers**, which can cause **precision errors**
        
    - Often implemented using **sine and cosine** rather than complex exponentials
      
      
### Cryptology

Cryptology is the science of **securing communication** through:

- **Cryptography**: creating secure messages
    
- **Cryptanalysis**: breaking or analyzing encrypted messages
    

---

### The Only Provably Unbreakable Cipher

#### **One-Time Pad**

- You generate a **random bitstream** the same length as your message.
    
- Then, you **XOR** the message with the bitstream (pad).
    
- **Encryption**:  
    C=M⊕KC = M \oplus KC=M⊕K (ciphertext = message XOR pad)
    
- **Decryption**:  
    M=C⊕KM = C \oplus KM=C⊕K
    

**Why it’s secure**:

- If the pad is truly random, never reused, and kept secret, it's **provably unbreakable**.
    

**Drawbacks**:

- You need a **new random pad for every message**.
    
- Requires **secure transmission of the pad**, which defeats the point of encryption if you're not careful.
    

---

### Number Theory Foundations (used in RSA)

Let m,nm, nm,n be positive integers.

#### **Divisibility**:

- m∣nm \mid nm∣n (read as "m divides n") if:
    
    n≡0 (mod m)n \equiv 0 \ (\text{mod } m)n≡0 (mod m)
    
    That is, no remainder when nnn is divided by mmm.
    

#### **Prime Numbers**:

- A number ppp is **prime** if its only positive divisors are **1** and **p**.
    
- Otherwise, it's **composite**.
    

#### **Unique Factorization Theorem (Fundamental Theorem of Arithmetic)**:

- Every integer n>1n > 1n>1 can be uniquely expressed as a product of prime powers:
    
    n=p1e1⋅p2e2⋅⋯⋅pkekn = p_1^{e_1} \cdot p_2^{e_2} \cdot \cdots \cdot p_k^{e_k}n=p1e1​​⋅p2e2​​⋅⋯⋅pkek​​
- Proved by **mathematical induction**.
    
- This is **critical** for RSA — factoring large numbers is hard, but multiplication is easy.
    

---

### There Are Infinitely Many Primes

**Theorem**:

- There are **infinitely many prime numbers**.
    

**Proof by contradiction (Euclid’s proof)**:

1. Assume there are only finitely many primes: p1,p2,...,pnp_1, p_2, ..., p_np1​,p2​,...,pn​
    
2. Let N=p1⋅p2⋅...⋅pn+1N = p_1 \cdot p_2 \cdot ... \cdot p_n + 1N=p1​⋅p2​⋅...⋅pn​+1
    
3. NNN is not divisible by any of the primes in the list → contradiction
    
4. So there must be more primes → **infinitely many**
    

---

### Fermat’s Little Theorem

- Let ppp be a **prime** and aaa an integer such that p∤ap \nmid ap∤a, then:
    
    ap−1≡1 (mod p)a^{p-1} \equiv 1 \ (\text{mod } p)ap−1≡1 (mod p)
- This is used in **RSA** to prove correctness of decryption.
    

---

### RSA Encryption

#### Overview

RSA is a **public-key encryption system** that relies on the difficulty of **factoring large integers**.

---

#### RSA Key Generation

1. **Choose two large primes**:
    
    p,qp, qp,q
2. Compute:
    
    n=p⋅qn = p \cdot qn=p⋅q
    - This is part of the **public key**
        
    - It's hard to factor back into ppp and qqq
        
3. Compute Euler’s **totient function**:
    
    ϕ(n)=(p−1)(q−1)\phi(n) = (p - 1)(q - 1)ϕ(n)=(p−1)(q−1)
    - This is the number of integers < nnn that are relatively prime to nnn
        
4. Choose an **encryption exponent** eee:
    
    1<e<ϕ(n),such that gcd⁡(e,ϕ(n))=11 < e < \phi(n), \quad \text{such that } \gcd(e, \phi(n)) = 11<e<ϕ(n),such that gcd(e,ϕ(n))=1
5. Compute the **decryption exponent** ddd:
    
    d≡e−1 (mod ϕ(n))d \equiv e^{-1} \ (\text{mod } \phi(n))d≡e−1 (mod ϕ(n))
    - This means: d⋅e≡1mod  ϕ(n)d \cdot e \equiv 1 \mod \phi(n)d⋅e≡1modϕ(n)
        

---

#### RSA Keys

- **Public key**: (e,n)(e, n)(e,n)
    
- **Private key**: (d,n)(d, n)(d,n)
    

---

#### Encryption and Decryption

- **Encrypt a message** MMM (where 0<M<n0 < M < n0<M<n):
    
    C=Memod  nC = M^e \mod nC=Memodn
- **Decrypt the ciphertext**:
    
    M=Cdmod  nM = C^d \mod nM=Cdmodn

**Why it works**:

- Based on Fermat's Little Theorem and Euler’s theorem:
    
    Med≡M (mod n)M^{ed} \equiv M \ (\text{mod } n)Med≡M (mod n)

---

### Why RSA Is Secure

- The security of RSA relies on the fact that **factoring nnn into ppp and qqq** is **computationally hard** when ppp and qqq are very large (hundreds or thousands of bits).
    
- While anyone can see eee and nnn, without knowing ppp and qqq, it's **infeasible to compute ϕ(n)\phi(n)ϕ(n)**, and thus **impossible to compute ddd** efficiently.


### **Complexity Theory**

### **Turing Machines**

- A **Turing Machine** is a theoretical model of computation used to define what can be computed.

- All major models of computation (like lambda calculus, RAM machines) are equivalent in power to Turing Machines.
    
- These models can represent **infinite sets** or behaviors using **finite descriptions** (like rules or instructions).
    

### **What Happens When You Run a Turing Machine?**

When you run a Turing machine, three things can happen:

1. It **halts and accepts** the input (good).
    
2. It **halts and rejects** the input.
    
3. It **runs forever** (bad — no useful output).
    

---

### **Recursive vs. Recursively Enumerable Languages**

|Language (L)|Complement (L̅)|Classification|
|---|---|---|
|Recursive|Recursive|Both recursive|
|R.E.|Not R.E.|Complement not R.E.|
|Not R.E.|Not R.E.|Neither is R.E.|

- A language is **recursive** if there exists a Turing machine that always halts and correctly answers **yes** or **no** for any input.
    
- A language is **recursively enumerable (R.E.)** if there's a Turing machine that:
    
    - **Halts and accepts** strings in the language.
        
    - Might **run forever** on strings not in the language.
        
- If a language is recursive, it's also R.E.
    
- If a language is R.E., its complement might not be.
    
- A language and its complement can't **both** be R.E. unless the language is actually recursive.
    

---

### **Deterministic vs. Nondeterministic Turing Machines**

|Feature|Deterministic TM|Nondeterministic TM|
|---|---|---|
|Behavior|One possible path|Multiple branching paths|
|Acceptance evidence|Yes|Yes|
|Time bound known?|Yes|Not necessarily|

---

### **P and NP**

- **P**: Class of problems solvable in **polynomial time** using a **deterministic Turing machine**.
    
- **NP**: Class of problems solvable in polynomial time by a **nondeterministic Turing machine**, or equivalently, problems where **given a solution**, we can **verify** it in polynomial time using a deterministic machine.
    

**P ⊆ NP**, because anything you can do deterministically, you can do nondeterministically.

**Is P = NP?** Nobody knows.

- If **P = NP**, it would mean that all the hard problems in NP can actually be solved efficiently — not just verified.
    

---

### **NP-Hard and NP-Complete**

- **Polynomial-Time Reducibility (≤ₚ)**:
    
    - We say a problem **L reduces to R** if we can transform instances of **L** into instances of **R** using a polynomial-time algorithm.
        
    - This shows **R is at least as hard** as **L**.
        
    - Important: Reductions are **one-way**, not symmetric.
        
- **NP-Hard**:
    
    - A problem **R** is NP-Hard if every problem in NP reduces to it.
        
    - In other words, R is at least as hard as **every** problem in NP.
        
- **NP-Complete**:
    
    - A problem is NP-Complete if it is:
        
        1. **NP-Hard**
            
        2. **Also in NP**
            

---

### **Boolean Satisfiability (SAT)**

- The **Boolean Satisfiability Problem** (SAT) asks:
    
    > Is there a way to assign true/false values to variables in a Boolean formula so that the formula evaluates to **true**?
    
- Example:

```
`(A ∨ B) ∧ (¬A ∨ C)`
```

- Try assigning A = false, B = true, C = false.
    
- (A ∨ B) = true, (¬A ∨ C) = true → formula is **satisfiable**.

- SAT was the **first problem shown to be NP-complete**, by **Stephen Cook** (1971) and independently by **Leonid Levin**. This result is known as the **Cook-Levin Theorem**.
    
    - It means that every problem in NP can be **converted into SAT** in polynomial time.
        
- SAT is often written in **Conjunctive Normal Form (CNF)**:
    
    - A conjunction (AND) of clauses, each of which is a disjunction (OR) of literals (variables or their negations).
        
    - Example:
```
`(A ∨ ¬B) ∧ (¬A ∨ C ∨ D)`
```

- **3-SAT** is a special case where each clause has exactly 3 literals.
    
    - Even **3-SAT** is NP-complete.
        
    - Many NP-completeness proofs reduce from 3-SAT.
        
- To prove your own problem is NP-hard, you show that SAT (or 3-SAT or another NP-complete problem) can be transformed into your problem using a polynomial-time reduction.
  
#### **Three Notions in Computational Problems**

In complexity theory, many problems can be framed in three related ways: **decision**, **optimization**, and **search**. These are different formulations of the same underlying problem and often relate to one another in interesting ways.

### 1. **Decision Problems**

- These are **yes/no** questions.
    
- The core of the **NP** complexity class — NP is defined in terms of decision problems.
    
- Solving the decision version can often help solve the other two forms.
    

### 2. **Optimization Problems**

- Goal is to **maximize or minimize** some objective.
    
- Often harder than decision versions because they require finding the **best** among many valid solutions.
    
- Typically not in NP unless the optimal solution can be verified efficiently.
    

### 3. **Search Problems**

- Given that a solution **exists**, find **one** such solution.
    
- Search problems often reduce to decision problems by binary search or iterative checking.
    

---

### **Examples**

#### 1. **Constrained Boolean SAT (e.g., "at most _k_ variables assigned True")**

- **Decision**: Is there an assignment of truth values to variables such that the formula is satisfied **and** at most **k** variables are set to **true**?
    
- **Optimization**: What is the **maximum number of clauses** that can be satisfied while keeping at most **k** variables true?
    
- **Search**: Given that such an assignment exists, **find** one.
    

> This version of SAT becomes a type of **constrained optimization** and can be much harder than standard SAT.

---

#### 2. **Longest Path Problem**

- **Definition**: Given a graph and two vertices **s** and **t**, what is the **longest simple path** from **s** to **t** (i.e., no repeated nodes)?
    
- **Decision**: Is there a simple path from **s** to **t** of length at least **k**?
    
- **Optimization**: What is the **maximum length** of a simple path between **s** and **t**?
    
- **Search**: Given a length **k**, **find** such a path if it exists.
    

> Note: The **longest path problem** in general graphs is **NP-hard** (unlike shortest path which is easy).

---

#### 3. **Vertex Cover**

- **Definition**: A **vertex cover** in a graph is a set of vertices such that every edge has at least one endpoint in the set.
    
- **Decision**: Does the graph have a vertex cover of size ≤ **k**?
    
- **Optimization**: What is the **minimum size** of a vertex cover?
    
- **Search**: **Find** a vertex cover of size ≤ **k**, assuming one exists.
    

> The decision version of vertex cover is **NP-complete**.
