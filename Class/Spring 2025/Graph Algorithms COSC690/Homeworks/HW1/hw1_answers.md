Name: Befikir T. Bogale
Class: COSC690 Graph Algorithms

### Question 1

**Draw a graph to represent the NYC metro area using the 5 labeled land masses and 19 bridges.**

![[nyc_graph.png]]

**Read the Konigsberg problem and apply similar reasoning to determine if it would be possible to start at some point, drive across all 19 NYC bridges and tunnels exactly once, and then return to your starting point.**

Euler showed that for a path to exist such that we drive across all NYC bridges and tunnels exactly once:
- At most two nodes can have an odd degree
	- Staten Island (3), New Jersey (5), and Manhattan (13) have an odd degree so this condition is unsatisfied.
- All other nodes must have an even degree

The first condition which states that at most two nodes can have an odd degree is unsatisfied, as such it is impossible for  a path to exist that drives across all NYC bridges and tunnels exactly once.

In order to ensure such a path exists the graph must be modified to to satisfy Euler's conditions. This can be done by simply adding a bridge between Long Island and Manhattan, as follows:
![[nyc_graph_solved.png]]


### Question 2

**Given the following adjacency matrix, draw the corresponding graph by hand and determine its minimum degree, maximum degree, and graph density.**


![[question_2_graph.png]]

The minimum degree is 2, of which nodes 1, 7, 4, and 3 consist of. 

The maximum degree is 5 which is held by node 6.

Since this is an undirected graph the graph density can be calculated by 2(12) / 9(9 - 1) = 0.33

### Question 3

**What is the minimum number of leaves a tree on n vertices may have? And the maximum?**

Calculating the minimum and maximum number of leaves on a tree with n verticies is kind of like constructing a piecewise function.

If the tree has one vertex then it has no edges and has a degree of zero. In such a case the minimum number of leaves is 0 as well as the maximum.

If a tree has 2 or more vertices then the minimum number of leaves it can have is 2. This can be verified by drawing a tree that is akin to a straight line, it will always have 2 leaves regardless of the number of vertices.

On the other hand, if a tree is arranged in a star like format we can deduce the maximum number of leaves, which is n - 1.

**Now describe an algorithm (do not program it) that takes as input such a tree and returns its number of leaves. A leaf in a graph is a vertex with degree 1.**

A program that takes a tree as input would operate as follows:
- Create a counter
-  Iterate through all the vertices 
	- If the degree is 1 then it is a leaf. (i.e number of edges is 1)
		- Increment counter
- return counter

