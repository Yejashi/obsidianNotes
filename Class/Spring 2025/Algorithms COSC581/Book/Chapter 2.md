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

I am going to give you sections of a text book. I want you to reduce the text to its most important bits, be detailed. This is from the text book: Introuduction to Algorithms.

## 2.2 Analyzing algorithms

# Understanding Algorithm Analysis

## The Purpose of Analysis

Algorithm analysis primarily focuses on predicting resource requirements, with computational time being the most common metric. This analysis helps identify the most efficient algorithm among several candidates and eliminate inferior options.

## The RAM Model

The Random Access Machine (RAM) model serves as the foundational framework for analyzing algorithms. Key characteristics include:

1. Sequential Execution: Instructions execute one after another without concurrent operations.
2. Constant Time Operations: Each basic instruction (arithmetic, data movement, control) takes constant time.
3. Data Types and Memory:
    - Supports integer, floating-point, and character data types
    - Boolean values typically represented as integers (0 for FALSE, nonzero for TRUE)
    - Word size is typically limited to c log₂ n bits (c ≥ 1) for input size n
    - Arrays stored in contiguous memory locations

## Important Considerations in Analysis

### Input Size

The choice of input size measure depends on the problem:

- For sorting: number of items (n)
- For integer operations: number of bits needed
- For graphs: combination of vertices and edges
- Some problems may require multiple parameters

### Running Time Analysis

Running time is measured by counting executed instructions and data accesses. Three key perspectives:

4. Best Case:
    - Represents minimum running time
    - Example: In insertion sort, occurs with already-sorted arrays
    - Running time: Θ(n)
5. Worst Case:
    - Represents maximum running time
    - More commonly analyzed due to:
        - Provides guaranteed upper bound
        - Often occurs in practical scenarios
        - More reliable for performance guarantees
    - For insertion sort: Θ(n²)
6. Average Case:
    - Represents expected performance on random inputs
    - Can be similar to worst case
    - Requires assumptions about input distribution
    - May benefit from randomized algorithms

## Order of Growth Analysis

This is the most practical way to understand algorithm efficiency:

7. Focus on Leading Terms:
    - Ignore lower-order terms
    - Disregard constant coefficients
    - Example: n²/100 + 100n + 17 simplifies to Θ(n²)
8. Asymptotic Notation:
    - Uses Θ (theta) notation
    - Θ(n²) means "roughly proportional to n² for large n"
    - Helps compare algorithms based on growth rate
    - More precise definitions appear in later chapters

This analysis framework provides a foundation for comparing algorithms and predicting their performance in practical applications. The focus on order of growth rather than exact running times makes the analysis both more manageable and more broadly applicable across different implementation environments.