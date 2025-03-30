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

