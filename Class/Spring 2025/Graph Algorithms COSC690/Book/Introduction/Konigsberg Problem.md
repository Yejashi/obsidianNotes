The Seven Bridges of Königsberg is a historically notable problem in mathematics.

The city of Königsberg in Prussia (now Kaliningrad, Russia) was set on both sides of the Pregel River, and included two large islands—Kneiphof and Lomse—which were connected to each other, and to the two mainland portions of the city, by seven bridges. 

![[Pasted image 20250126151657.png]]

The problem was to devise a walk through the city that would cross each of those bridges **once and only once**.

Leonhard Euler resolved the problem in 1736 by proving that no such walk could exist. His work **laid the foundations for graph theory**, an area of mathematics that studies **networks and their relationships**.

Euler's method for proving this was groundbreaking because it introduced a way to analyze the problem mathematically, using the concept of nodes (representing landmasses) and edges (representing bridges).

### In-Depth Breakdown

In graph theory, the Seven Bridges of Königsberg problem is a perfect example of a problem that can be represented as a graph. A graph consists of two main components: **nodes** (or vertices) and **edges** (the connections between the nodes).

**Graph Representation of the Problem**
- The **nodes** represent the landmasses in the city: the two islands (Kneiphof and Lomse) and the two mainland sections.
- The **edges** represent the seven bridges connecting these landmasses.

**Euler's Insight**
To understand why the problem cannot be solved, Euler came up with a few key concepts:
- **Even Degree**: A node has an even degree if the number of edges (or bridges) connected to it is an even number.
- **Odd Degree**: A node has an odd degree if the number of edges (or bridges) connected to it is an odd number.

For a path to exist that crosses each bridge exactly once, Euler showed that:
1. **At most two nodes can have an odd degree** (these would be the starting and ending points of the path).
2. **All other nodes must have an even degree**.

If more than two nodes have an odd degree, no such path exists.

