## Question 1
![[Pasted image 20250305123601.png]]

The maximum flow is 4.

## Question 2

![[Pasted image 20250305143833.png]]
a.) The edge connectivity of the undirected graph is 2. This can be found by converting it to a directed graph where all the edges are bidirectional and have a capacity of 1. Then it's simply a matter of finding the maximum network flow and and using the max flow min cut theorem.

b.) It suffices to arbitrarily set s and let the other vertices play the role of t because not matter the value of s, you will eventually have to consider the verticies for t that produce the minimum max flow so that you can determine the edge connectivity. As such, it's better to simply choose an arbitray s and figure out the rest later.
