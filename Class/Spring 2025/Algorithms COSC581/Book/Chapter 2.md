## 2.1 Insertion Sort
### **Insertion Sort Overview**

Insertion Sort is a simple algorithm for sorting an array by iteratively placing each element into its correct position relative to already sorted elements. The input consists of an array of _n_ numbers, and the output is a reordered array in non-decreasing order. Sorting often involves _keys_ associated with additional _satellite data_, such as student records with attributes like GPA and age.

### **Concept and Analogy**

The algorithm works similarly to sorting playing cards in hand:

1. Start with an empty left hand and pick the first card.
2. Take the next card from the pile and insert it into the correct position among the sorted cards in the left hand.
3. Repeat for all cards, always maintaining a sorted order in the left hand.

### Pseudocode for Insertion Sort

```cpp
INSERTION-SORT(A, n)
1 for i = 2 to n
2   key = A[i]  
3   // Insert A[i] into the sorted subarray A[1:i-1]  
4   j = i - 1  
5   while j > 0 and A[j] > key  
6       A[j + 1] = A[j]  
7       j = j - 1  
8   A[j + 1] = key  

```

Each iteration selects a new element (key) and shifts larger elements to the right until the key is placed in its correct position.

### **Loop Invariants and Correctness Proof**

A **loop invariant** helps prove correctness by ensuring the following properties:

- **Initialization:** Before the first iteration, the subarray `A[1]` is trivially sorted.
- **Maintenance:** Each step inserts a new element into the correct position while keeping the previous elements sorted.
- **Termination:** When the loop ends, `A[1:n]` is fully sorted.

Loop invariants provide a structured way to verify algorithm correctness, similar to mathematical induction, where:

- The **base case** ensures correctness at the start.
- The **inductive step** proves correctness for subsequent iterations.
- The **termination condition** confirms that when the loop exits, the desired result holds.

### **Pseudocode Conventions**

- **Indentation** defines block structures instead of curly braces or keywords like `begin`/`end`.
- **Loop behavior** resembles that in C, C++, Java, and Python. Unlike some languages, the loop variable retains its final value after iteration ends.

### **Summary**

Insertion Sort is an efficient algorithm for small datasets, working by incrementally growing a sorted subarray. Its correctness is verified using loop invariants, and its implementation follows a structured pseudocode convention.