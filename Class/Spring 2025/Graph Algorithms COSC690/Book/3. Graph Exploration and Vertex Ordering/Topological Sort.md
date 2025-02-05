Topological sorting is a method for linearly ordering the vertices of a directed graph so that for every directed edge from vertex u to vertex v, u comes before v in the ordering. 

In other words, it produces a sequence in which tasks (or nodes) are arranged such that every dependency is respected. 

This concept is central in many applications like scheduling tasks, resolving dependencies in makefiles, or ordering cells in a spreadsheet for recalculation.

Definition and Key Properties:
- **Directed Acyclic Graph (DAG):**  
    A topological sort is only possible for a graph with no directed cycles. Such graphs are known as Directed Acyclic Graphs (DAGs). The absence of cycles guarantees that there is at **least one vertex with no incoming edge**, which is essential for initiating the sort process.
- **Linear Ordering:**  
    In a valid topological ordering, every edge (u, v) implies that u appears before v in the sequence. This ordering provides a way to schedule or arrange tasks so that prerequisites are completed before the tasks that depend on them [​].