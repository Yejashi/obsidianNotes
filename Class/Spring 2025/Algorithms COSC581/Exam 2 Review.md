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