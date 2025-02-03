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

