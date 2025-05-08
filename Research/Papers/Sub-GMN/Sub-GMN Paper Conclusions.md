[TODO]

### Future Work

#### Scaling to very large graphs
Sub-GMN works well in their synthetic experiments (graphs of up to ~300 nodes).
BUT → real-world graphs (social networks, large molecules, knowledge graphs) can be millions of nodes.
->  Sub-GMN will need more research to:
- Improve scalability
- Improve accuracy on very large graphs
Possible solutions → smarter batching, hierarchical matching, sampling, etc.


#### Cross-graph propagation mechanism
Currently -> Sub-GMN treats:
- Query graph → GCN → embeddings
- Data graph → GCN → embeddings
Then → they are compared via NTN + Attention.

But → this process does not directly allow information to flow between the query graph and data graph while embedding.
→ Possible limitation → may miss subtle relationships that require considering query+data graph together at embedding time.

**Cross-graph propagation** → a new research direction → allows embeddings of query graph nodes to directly interact with embeddings of data graph nodes during message passing.