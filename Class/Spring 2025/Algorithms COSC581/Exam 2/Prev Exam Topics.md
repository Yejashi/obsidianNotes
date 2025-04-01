## Huffman Coding

Design a Huffman Code for a text file.
- **Count the frequency of each character** in the input data.
    - This gives you a frequency table (e.g., `{'a': 5, 'b': 9, 'c': 12, 'd': 13, 'e': 16, 'f': 45}`).
- **Create a priority queue (min-heap)** of nodes.
    - Each node is a leaf node containing a character and its frequency.
    - Nodes with lower frequencies have higher priority (min-heap).
- **Build the tree**:
    - While there is more than one node in the queue:
        1. Remove the two nodes with the **lowest frequency**.
        2. Create a new internal node with:
            - Frequency = sum of the two nodes' frequencies.
            - Left child = first node removed.
            - Right child = second node removed.
        3. Add this new node back into the priority queue.
- **Repeat until one node remains** in the queue.
    - This node becomes the **root** of the Huffman Tree.
- **Traverse the tree** to assign binary codes:
    - Moving left = add '0' to the code.
    - Moving right = add '1'.
    - The resulting binary codes are the Huffman codes for each character.
### Network Flow
Given an adjacency matrix, use network flow (maximum flow) to find a perfect bipartite matching.

[How to do it: 1](https://www.youtube.com/watch?v=HWHjQdNC-7Y&t=131s)
[How to do it: 2](https://www.youtube.com/watch?v=x2BdRml5lmc)

[Maximum Flow with Ford Fulkerson ](https://www.youtube.com/watch?v=HWHjQdNC-7Y&t=131s)


### Linear Programming

Step 1. Convert to standard form
- If minimization, multiply by -1.
Step 2. Convert to slack form.
- Left = basic vars
- Right = non basic vars
Step 3. In objective function, choose non basic variable that can contribute the most.
- Largest positive positive coefficient [A]
