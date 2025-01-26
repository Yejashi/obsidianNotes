In computer science, a graph is an abstract data type that is meant to implement the undirected graph and directed graph concepts from the field of graph theory within mathematics. 

### Basic Operations
The basic operations provided by a graph data structure _G_ usually include:
- adjacent(_G_, _x_, _y_): tests whether there is an edge from the vertex _x_ to the vertex _y_;
- neighbors(_G_, _x_): lists all vertices _y_ such that there is an edge from the vertex _x_ to the vertex _y_;
- add_vertex(_G_, _x_): adds the vertex _x_, if it is not there;
- remove_vertex(_G_, _x_): removes the vertex _x_, if it is there;
- add_edge(_G_, _x_, _y_, _z_): adds the edge _z_ from the vertex _x_ to the vertex _y_, if it is not there;
- remove_edge(_G_, _x_, _y_): removes the edge from the vertex _x_ to the vertex _y_, if it is there;
- get_vertex_value(_G_, _x_): returns the value associated with the vertex _x_;
- set_vertex_value(_G_, _x_, _v_): sets the value associated with the vertex _x_ to _v_.

Structures that associate values to the edges usually also provide:
- get_edge_value(_G_, _x_, _y_): returns the value associated with the edge (_x_, _y_);
- set_edge_value(_G_, _x_, _y_, _v_): sets the value associated with the edge (_x_, _y_) to _v_.

### Common data structures for graph representation

Adjacency list[2]
    Vertices are stored as records or objects, and every vertex stores a list of adjacent vertices. This data structure allows the storage of additional data on the vertices. Additional data can be stored if edges are also stored as objects, in which case each vertex stores its incident edges and each edge stores its incident vertices.
Adjacency matrix[3]
    A two-dimensional matrix, in which the rows represent source vertices and columns represent destination vertices. Data on edges and vertices must be stored externally. Only the cost for one edge can be stored between each pair of vertices.
Incidence matrix[4]
    A two-dimensional matrix, in which the rows represent the vertices and columns represent the edges. The entries indicate the incidence relation between the vertex at a row and edge at a column.

