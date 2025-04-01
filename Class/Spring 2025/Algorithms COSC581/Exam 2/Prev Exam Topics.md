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
**Given an adjacency matrix, use network flow (maximum flow) to find a perfect bipartite matching.**

[How to do it: 1](https://www.youtube.com/watch?v=HWHjQdNC-7Y&t=131s)
[How to do it: 2](https://www.youtube.com/watch?v=x2BdRml5lmc)

[Maximum Flow with Ford Fulkerson ](https://www.youtube.com/watch?v=HWHjQdNC-7Y&t=131s)

**Use network flow (show your work) to find a 4 x 4 Boolean matrix whose row sums are (2,2,2,3) and whose column sums are (1,2,3,3), if any such a matrix exists.** 


### Linear Programming

Step 1. Convert to standard form
- If minimization, multiply by -1.
Step 2. Convert to slack form.
- Left = basic vars
- Right = non basic vars
Step 3. In objective function, choose non basic variable that can contribute the most.
- Largest positive positive coefficient [A]
Step 4. Choose constraing with tightest bound [B]
- Min ratio role, which [A] hits zero first
Step 5. Pivot [A] with [B], rewrite [A] as [B]
- Plug in [A] into all equations

### Fast Fourier Transform
The FFT can reduce the time to multiply  polynomials to $\Theta(nlgn)$ 

**Time domain:** A function mapping time to amplitude.

**Frequency Domain:** Represents a signal in terms of it's constituent frequencies.
- Shows how much of the signal lies within each frequency band.

**Horner's Rule:** Rewrites the polynomial so that i can be evaluated faster.
- Factor it out into parenthesis and solve starting form the inner most parentheses.
- Instead of A(x) = $a_{0}+a_1x+a_2{x^2}+a_3x^3$   
- Do: A(x) = $a_{0}+ x(a_1+x(a_2+x(a_3)))$ 
- Now, no exponents, just multiplications and additions

**Point Value Representation:** Instead of writing a polynomial using coefficient, you can describe them as a list of inputs and outputs.

**Interpolation:** If you want to go back to coefficient form from point value pairs
- coefficient -> point value = Evaluation (plug in values)
- point value -> coefficient = Interpolation (find formula)

How to use FFT to multiply two polynomials.
- Switch from coefficient representation to point by value representation.

![[Pasted image 20250401003857.png]]

**The Fast Fourier Transform. Explain where in its derivation the FFT employs mathematical symmetry to multiply two polynomials of degree n in O(nlogn) time.**

![[Pasted image 20250401004928.png]]


### Complexity Theory

What is the Satisfiability Problem?
- The **satisfiability** problem asks whether there exists a truth assignment to variables that makes a given Boolean formula true.

What does it mean to say that a problem is NP-hard?
- A problem is **NP-hard** if every problem in NP can be reduced to it in polynomial time, meaning it is at least as hard as the hardest problems in NP.

What does it mean to say that a problem is NP-complete?
- A problem is **NP-complete** if it is both in NP and NP-hard.

State the Cook-Levin Theorem?
- The **Cook-Levin Theorem** states that the Boolean satisfiability problem (SAT) is NP-complete.

### Cryptology

Background:



![[Pasted image 20250401011249.png]]

**Encode message 3 in RSA crypto system with n = 91 and E = 5**

**Consider an RSA crypto scheme with n = 35 and E = 5.**
- List a valid value for D.
- Encode messages 3, 4 and 5.
- List two messages that are always unencryptable.
	- 0 and 1.
- List another message unencryptable under this scheme.