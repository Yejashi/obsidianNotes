### Introduction
Subgraph matching is a fundamental problem in graph data management. Given a data graph 𝐺 and a query graph 𝑄, a subgraph matching asks for all subgraphs (also called embeddings or matches) in 𝐺 that match 𝑄 in terms of isomorphism. 

Prior works on the exact subgraph matching problem usually followed the exploration-based or the join-based methodology . The exploration-based methods adopt the backtracking search, which maps query nodes to data nodes and iteratively extends intermediate results to find all matches. The join-based methods convert the subgraph query to a relational query, and evaluate the multi-way join to obtain all results.

**Our Contributions:** In this paper, we study the exact subgraph matching problem on the large-scale data graph and propose a novel GNN-AE (GNN-based Anchor Embedding) framework for exact and efficient subgraph matching. In contrast to existing GNN-based approaches for approximate subgraph matching without theoretical guarantees of accuracy, our GNN-AE can obtain exact results for subgraph matching and retrieve the locations of all matches.

![[Pasted image 20250427134334.png]]

As shown in Figure 2, in GNN-AE, we first propose a series of concepts related to anchor, including anchor, anchor graph/path, etc. We design effective anchor embedding techniques (including anchor graph embedding, and anchor path embedding) based on anchor concepts and GNN models, which transform the subgraph matching problem into a search problem in the embedding space.

