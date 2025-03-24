### Motivation

Fluxion, while effective for many workloads, has inherent scalability limitations due to its reliance on depth-first search (DFS) during resource traversal and matching. As we approach the later stages of the Fractale project—especially with its multi-cluster scheduling needs—these limitations are expected to hinder throughput and efficiency.

Moreover, Fluxion’s current constraint satisfaction mechanism is not well-suited for mixed-integer linear programming (MILP)-style problems, limiting its adaptability in complex scheduling scenarios.

---

### Proposal

Explore whether a Graph Neural Network (GNN) can be used to approximate Fluxion's resource matching process on a simplified scale. The idea is to replace the DFS-based matching in Fluxion with a learned model that can infer subgraph matches more efficiently.

#### High-Level Plan

1. **Describe and model Fluxion’s behavior:**
    - Explain how DFS is used for resource traversal and job matching.
    - Model a simple resource graph (e.g., nodes, cores, sockets, GPUs) used by Fluxion.
        
2. **GNN-based Subgraph Matching:**
    - Implement a GNN approach to perform subgraph isomorphism.
    - Compare GNN-generated matches to those produced by Fluxion.
    - Determine whether the GNN can reliably reproduce identical or similar matches.
        
3. **Experimental Setup:**
    - Start with a small-scale resource graph:
        - ~10 nodes, each with 18 cores.
        - A few job specifications with varying resource needs.
            
    - Fix the resource graph and evaluate how the GNN allocates jobs versus how Fluxion would.

---

### Key Constraints & Considerations

- **Accuracy of Matching:**  
    GNN output must not produce multiple conflicting matches for the same resource. For example:
    - If Job A is assigned to Node X, then Job B cannot be assigned to Node X as well unless explicitly allowed.
    - Strong constraints must be encoded into the model to avoid invalid resource contention.
        
- **Constraint Encoding in GNNs:**
    - Explore techniques from domains like drug discovery where hard constraints are common.
    - Consider post-processing or hybrid methods (e.g., using GNN output as input to a real Flux queue for validation).
        

---

### Goals of the Project

1. **Survey the Landscape:**
    - History and challenges of subgraph isomorphism.
    - Review prior work on neural networks applied to graph matching and scheduling problems.

2. **Model Development:**
    - Design and implement a GNN that represents the resource graph.
    - Encode job specifications and query the GNN for matching outputs.

3. **Evaluation & Comparison:**
    - Compare the GNN-based scheduling to Fluxion’s native DFS-based approach.
    - Measure output match quality, constraint satisfaction, and time-to-match.
        

---

### Next Steps

- **Step 1:** Represent the resource graph using a GNN-friendly structure (nodes with attributes like cores, sockets, etc.).
    
- **Step 2:** Train the GNN to learn matching behavior using job-resource pairs from Fluxion.
    
- **Step 3:** Evaluate accuracy—what outputs are acceptable (matching Fluxion), and what deviations are not.