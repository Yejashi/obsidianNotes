## Question 1
![[Pasted image 20250305123601.png]]

The maximum flow is 4.

## Question 2

![[Pasted image 20250305143833.png]]
a.) The edge connectivity of the undirected graph is 2. This can be found by converting it to a directed graph where all the edges are bidirectional and have a capacity of 1. Then it's simply a matter of finding the maximum network flow and and using the max flow min cut theorem.

b.) It suffices to arbitrarily choose s and allow the other vertices to serve as t because, regardless of the choice of s, the calculation must ultimately account for the vertex t that yields the minimum maximum flow. This approach ensures that the edge connectivity is accurately determined while simplifying the process by avoiding the need to evaluate every possible s-t pair.

## Question 3