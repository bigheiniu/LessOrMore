## Essentials about graph



1. Graph

   __Basic Component__: Nodes, Edge, Degress and Degree distribution

   __Graph Representation__: Adjacency Matrix, Adjacency List, Edge List. 

   >Adjacency is often used to matrix decomposition, to find similarities, stability of function. And we can consider a martix as linear function. In this way, if adjancency matrix multiply other matrix or vectors, it just use information in ordinary matrix space.

   __Types of Graphs__: Null Graph, Empty Graph, Simple Graphs and Multiple Graphs, Weighted Graphs.

   __Measures__: Connectivity -> (Traveling an edge \\ Walk, Path, Trail, Tour and Cycle)

   __Graph Algorithms__: 

     - DFS, BFS

     - Prim's Algorithm: Grow the Spanning Tree with Least weight. Select a random points as start point, and push this point into spaning tree. In the following iteration, the algorothms will find the least weight value among node in spanning tree and out side spanning tree.
     - Network Flow Algorithms: Maxmum use the flow-- increase the flow and it will not exceed the capacity. 

   2. Network

      __Degree Centrality__: rely on degree, in or out 

      __Eigenvector Centrality__: biggest eigenvalues impiles the corresponding vectors contain the most information in new basis space. And this will tell the most information of these graphs.

      __Katz Centrality__: similar to Eigenvector Centrality, but add a smooth constant

      __Page Rank__: once a node becomes an authority, it passes all its centrality along all of its out-links

      __Betweenness Centrality__: how important nodes are in connecting other nodes(for a node $v_i$ , is to compute the number of shortest paths between other nodes that pass through $v_i$)

      __Closeness Centrality__: the more central nodes are, the more quickly they can reach other nodes





	__Transitivity__: when a friend of my friend is my friend

	__Reciprocity__: If you become my friend, I'll be yours