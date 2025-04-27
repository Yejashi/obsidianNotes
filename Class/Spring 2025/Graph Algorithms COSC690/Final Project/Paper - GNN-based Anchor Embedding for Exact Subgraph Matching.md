### Introduction

Subgraph matching is a fundamental problem in graph data management. Given a data graph 𝐺 and a query graph 𝑄, a subgraph matching asks for all subgraphs (also called embeddings or matches) in 𝐺 that match 𝑄 in terms of isomorphism. 

Prior works on the exact subgraph matching problem usually followed the exploration-based or the join-based methodology . The exploration-based methods adopt the backtracking search, which maps query nodes to data nodes and iteratively extends intermediate results to find all matches. The join-based methods convert the subgraph query to a relational query, and evaluate the multi-way join to obtain all results.

