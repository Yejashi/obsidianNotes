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


### **Boolean Matrix Decidability**

---

### **Problem Statement**

- You are given:
    
    - A set of **row sums**: {r1,r2,...,rm}\{r_1, r_2, ..., r_m\}{r1​,r2​,...,rm​}
        
    - A set of **column sums**: {c1,c2,...,cn}\{c_1, c_2, ..., c_n\}{c1​,c2​,...,cn​}
        
    - Where:
        
        ∑i=1mri=∑j=1ncj\sum_{i=1}^{m} r_i = \sum_{j=1}^{n} c_ji=1∑m​ri​=j=1∑n​cj​
        
        (This is necessary — total number of 1s in the matrix from rows must equal that from columns)
        
- **Goal**: Decide whether there exists a **Boolean matrix** (i.e., a matrix with only 0s and 1s) of size m×nm \times nm×n such that:
    
    - Each row iii contains exactly rir_iri​ ones.
        
    - Each column jjj contains exactly cjc_jcj​ ones.
        

---

### **Approach: Reduce to a Network Flow Problem**

To solve this decision problem, we model it using **network flow**, which helps verify whether the row and column constraints can all be satisfied at the same time.

---

### **Steps to Convert to a Flow Network**

#### 1. **Construct a Bipartite Graph**

- Create a **bipartite graph** with:
    
    - **m nodes** on the left, one for each **row**.
        
    - **n nodes** on the right, one for each **column**.
        
- Draw an **edge** from each row node RiR_iRi​ to each column node CjC_jCj​:
    
    - This forms a **complete bipartite graph**.
        
    - Each edge represents a potential **1** at position (i,j)(i, j)(i,j) in the matrix.
        

#### 2. **Add Artificial Source and Sink**

- Add a **source node (s)** and a **sink node (t)** to model the flow.
    
- Connect:
    
    - **s → each row node RiR_iRi​** with capacity rir_iri​
        
        - This ensures that **each row has exactly rir_iri​ ones**.
            
    - **Each column node CjC_jCj​ → t** with capacity cjc_jcj​
        
        - This ensures that **each column has exactly cjc_jcj​ ones**.
            

#### 3. **Assign Capacities Between Row and Column Nodes**

- Set **capacity = 1** on each edge from row nodes to column nodes:
    
    - Ri→CjR_i \rightarrow C_jRi​→Cj​ has capacity 1.
        
    - This reflects that **at most one 1 can be placed at position (i,j)(i, j)(i,j)** in a Boolean matrix.
        

---

### **Final Network Summary**

- Vertices:
    
    - sss → source
        
    - R1,R2,...,RmR_1, R_2, ..., R_mR1​,R2​,...,Rm​ → row nodes
        
    - C1,C2,...,CnC_1, C_2, ..., C_nC1​,C2​,...,Cn​ → column nodes
        
    - ttt → sink
        
- Edges:
    
    - s→Ris \rightarrow R_is→Ri​: capacity rir_iri​
        
    - Ri→CjR_i \rightarrow C_jRi​→Cj​: capacity 1
        
    - Cj→tC_j \rightarrow tCj​→t: capacity cjc_jcj​
        

---

### **Solving the Problem**

- **Run the Ford-Fulkerson algorithm** (or any max-flow algorithm).
    
- **Check the value of the maximum flow** from sss to ttt.
    

---

### **Decision Condition**

- If the **maximum flow equals the total number of 1s**, i.e.,
    
    flow=∑i=1mri=∑j=1ncj\text{flow} = \sum_{i=1}^{m} r_i = \sum_{j=1}^{n} c_jflow=i=1∑m​ri​=j=1∑n​cj​
    
    then **Yes**:
    
    - A Boolean matrix with the given row and column sums **does exist**.
        
- If the flow is **less** than that total, then **No**:
    
    - Such a matrix **cannot** be constructed — there’s a conflict between row and column constraints.
        

---

### **Why This Works**

- The flow represents assigning 1s in the matrix:
    
    - Flow from RiR_iRi​ to CjC_jCj​ = 1 means matrix position (i,j)=1(i, j) = 1(i,j)=1.
        
- Constraints are enforced by the capacities:
    
    - Row constraints are enforced by source-to-row capacities.
        
    - Column constraints are enforced by column-to-sink capacities.
        
    - Only Boolean values are allowed because intermediate arc capacities are 1.
        

---

### **Example**

Suppose:

- Row sums: {2,1}\{2, 1\}{2,1}
    
- Column sums: {1,1,1}\{1, 1, 1\}{1,1,1}
    

We want a 2×32 \times 32×3 Boolean matrix such that:

- First row has two 1s.
    
- Second row has one 1.
    
- Each column has exactly one 1.
    

We’d construct:

- Source sss → row1 (capacity 2), row2 (capacity 1)
    
- row1/row2 → each of 3 column nodes (capacity 1)
    
- Each column → sink ttt (capacity 1)
    

If the max flow is 3, a valid matrix exists.