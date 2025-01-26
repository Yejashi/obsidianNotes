An **adjacency matrix** is another way to represent a graph using a 2D array (or matrix). In this representation, the graph's vertices are represented as both the rows and columns of the matrix, and the matrix elements indicate whether there is an edge between a pair of vertices.

### Key Characteristics of an Adjacency Matrix:
1. **Vertices**: The graph has **n** vertices, and the adjacency matrix is an **n × n** matrix, where each row and column corresponds to a vertex.
2. **Edges**: The matrix entries indicate whether there is an edge between two vertices.
    - In an **undirected graph**, the matrix is symmetric, meaning if there is an edge between vertex **i** and vertex **j**, both **A[i][j]** and **A[j][i]** will be non-zero.
    - In a **directed graph**, the matrix is not necessarily symmetric. If there is a directed edge from vertex **i** to vertex **j**, only **A[i][j]** will be non-zero, not **A[j][i]**.
3. **Matrix Entries**: The matrix entries are usually:
    - **1** (or any other non-zero value) if there is an edge between the corresponding vertices.
    - **0** if there is no edge between the corresponding vertices.
    - Sometimes, other values (such as weights) are used instead of 1 to indicate edge weights in weighted graphs.

