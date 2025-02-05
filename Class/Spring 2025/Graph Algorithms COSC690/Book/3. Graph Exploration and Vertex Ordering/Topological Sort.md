Topological sorting is a method for linearly ordering the vertices of a directed graph so that for every directed edge from vertex u to vertex v, u comes before v in the ordering. 

In other words, it produces a sequence in which tasks (or nodes) are arranged such that every dependency is respected. 

This concept is central in many applications like scheduling tasks, resolving dependencies in makefiles, or ordering cells in a spreadsheet for recalculation.

**Definition and Key Properties:**
- **Directed Acyclic Graph (DAG):**  
    A topological sort is only possible for a graph with no directed cycles. Such graphs are known as Directed Acyclic Graphs (DAGs). The absence of cycles guarantees that there is at **least one vertex with no incoming edge**, which is essential for initiating the sort process.
- **Linear Ordering:**  
    In a valid topological ordering, every edge (u, v) implies that u appears before v in the sequence. This ordering provides a way to schedule or arrange tasks so that prerequisites are completed before the tasks that depend on them.

## **Algorithms for Topological Sorting**

Two primary algorithms are widely used to compute a topological sort:

### 1. Kahn's Algorithm

- **Idea:**  
    Kahn's algorithm builds the sorted list by repeatedly removing nodes that have no incoming edges.
- **Steps:**
    1. **Initialize:** Identify all vertices with no incoming edges and insert them into a set S.
    2. **Process:** While S is not empty, remove a vertex n from S, append it to the list L (which will become the topologically sorted order), and then remove all edges emanating from n. If removing an edge causes another vertex to have no incoming edges, add that vertex to S.
    3. **Cycle Detection:** If edges still remain after processing, it indicates that the graph contains at least one cycle, and a topological sort is impossible [​].

### 2. Depth-First Search (DFS) Based Algorithm

- **Idea:**  
    This approach uses recursion to explore the graph. Each node is visited and, once all its dependencies (i.e., outgoing edges) are recursively processed, it is added to the front of the sorted list.
- **Steps:**
    1. **Initialization:** Begin with an empty list L and an unmarked set of nodes.
    2. **Recursive Visit:** For each unvisited node, perform a DFS. Mark nodes temporarily during the visit to detect cycles, and once all adjacent nodes have been fully explored, mark the node permanently and prepend it to L.
    3. **Ordering Guarantee:** Because nodes are added to L only after all nodes that depend on them have been processed, the resulting list is a valid topological order [​].