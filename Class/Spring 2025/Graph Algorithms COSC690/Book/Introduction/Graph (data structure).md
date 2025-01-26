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

