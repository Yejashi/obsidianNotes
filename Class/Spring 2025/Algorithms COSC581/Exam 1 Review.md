
### 1. Asymptotics

##### Asmptotic Notation
f = $\Theta(g)$
- f grows at the same rate as g
$f = O(g)$ 
- f grows no faster than g
$f = \Omega(g)$
- f grows at least as fast as g
$f = o(g)$ 
- f grows strictly slower than g
$f = \omega(g)$ 
- f grows faster than g
f ~ g
- f / g approaches 1

##### Limits
$\lim_{n \to \infty} \frac{f(n)}{g(n)} \neq 0, \infty$
- $f = \Theta(g)$

$\lim_{n \to \infty} \frac{f(n)}{g(n)} \neq \infty$
- $f = O(g)$

$\lim_{n \to \infty} \frac{f(n)}{g(n)} \neq 0$
- $f = \Omega(g)$

$\lim_{n \to \infty} \frac{f(n)}{g(n)} = 1$
- f ~ g

$\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0$
- $f = o(g)$

$\lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty$
- $f = \omega(g)$

##### L'hopital's rule
if $\lim_{n \to \infty} f(n) = \infty$ and $\lim_{n \to \infty} g(n) = \infty$ 
	then: $\lim_{n \to \infty} \frac{f'(n)}{g'(n)}$ = $\lim_{n \to \infty} \frac{f^\prime(n)}{g^\prime(n)}$

![[Pasted image 20250217221427.png]]



### 2. Master Theorem & Solving Recurrances

Let $a \geq 1$ and $b > 1$  be constants, let $f(n)$ be a function, and let $T(n)$ defined by the recurrence:
	$T(n) = aT\left(\frac{n}{b}\right) + f(n)$ 
where we intercept $n/b$ to be ceil($n/b$) or floor($n/b$).

Then $T(n)$ has the following asymptotic bounds:
- **Case 1:** if $f(n) = O(n^{log_{b}a - \epsilon})$  for some constant $\epsilon > 0$, then:
		$T(n) = \Theta(n^{log_{b}a})$ 
- **Case 2:** if $f(n) = \Theta(n^{log_{b}a})$ , then:
		$T(n) = \Theta(n^{log_{b}a}lgn)$ 
- **Case 3:** if $f(n) = \Omega(n^{log_{b}a + \epsilon})$  for some constant $\epsilon > 0$, AND if $af(n/b) \leq cf(n)$ for some c < 1 as n -> $\infty$ , then:
		$T(n) = \Theta(f(n))$ 

Examples for each case:
	**Case 1:**
		$T(n) = 2T\left(\frac{n}{4}\right)+ 1$ 
		a = 2, b = 4, f(n) = 1
		$n^{log_{4}2} = n^{1/2}$ 
		$O(n^{\frac{1}{2} - 1})$  = $O(1)$ 
		lim $1/1$ = 1 does not equal $\infty$  = O(1)
		$T(n) = \Theta(n^{1/2})$
	**Case 2:**
		$T(n) = 16T(\frac{n}{4}) + n^2$ 
		a = 16 b = 4 f(n) = $n^2$ 
		$n^{log_{4}16}$ = $n^2$
		$f(n) = \Theta(n^2)$ 
		lim $n^2/n^2$ = 1 does not equal $\infty, 0$ 
		$T(n) = \Theta(n^2lgn)$ 
	**Case 3:**
		$T(n) = 2T\left(\frac{n}{2}\right)+ \Theta(n^2)$ 
		a = 2 b = 2 f(n) = $\Theta(n^2)$ 
		$n^{log_{2}2} = n^1$ 
		f(n) = $\Theta(n^{2)} = \Omega(n^{1 + 1})$ 
		lim $n^2/n^2$ = 1 does not equal 0
		$2f\left(\frac{n}{2}\right) \leq \frac{1}{2}n^2$   n-->$\infty$
		T(n) = $\Theta(n^2)$ 

### 3. Sorting

| Algorithm                               | Key Comparisons | Record Moves | Extra Space | Stability | Simplicity | Best Case    | Average Case |
| --------------------------------------- | --------------- | ------------ | ----------- | --------- | ---------- | ------------ | ------------ |
| **Bubble Sort**                         | O($n^2$)        | O($n^2$)     | No          | Yes       | Very       | O($n$)       | ?            |
| **Insertion Sort (Straight)**           | O($n^2$)        | O($n^2$)     | No          | Yes       | Very       | O($n$)       | ?            |
| **Insertion Sort (Binary, Huge Files)** | O($n\log n$)    | O($n^2$)     | No          | Yes       | Yes-ish    | O($n$)       | O($n\log n$) |
| **Counting Sort** (Knuth’s version)     | O($n^2$)        | O($n$)       | Yes         | Yes       | Yes        | O($n^2$)     | O($n^2$)     |
| **Shell Sort (Diminishing Increment)**  | O($n^{1.5}$)    | ?            | No          | No        | No         | ?            | ?            |
| **Merge Sort**                          | O($n\log n$)    | O($n\log n$) | Yes         | Yes       | Yes        | O($n\log n$) | O($n\log n$) |
| **Heap Sort**                           | O($n\log n$)    | O($n\log n$) | No          | No        | Not really | O($n\log n$) | O($n\log n$) |
| **Quick Sort**                          | O($n^2$)        | O($n^2$)     | No          | No        | No         | O($n\log n$) | ?            |
| **Radix Sort**                          | O($$)           | O($$)        | No          | No        | No         | O($$)        | ?            |
| **Bucket Sort**                         | O($$)           | O($$)        | No          | No        | No         | O($$)        | ?            |

##### **Call sequences for some sorting algorithms :**
- Merge sort
	- merge sort
	- merge sort
	- merge
- quicksort
	- partition
	- quicksort
	- quicksort
- Heap sort (build the heap)
	- heapify
	- sort

##### Count sort
Counting sort is a non‐comparison sorting algorithm that works by “counting” how many times each value appears in your input, then using that information to directly place each item into its correct position in the output array. 

**List of 5 items**:
Imagine you have a small list (say, 5 items) where the keys (or values) come from a limited range.

Counting sort is particularly efficient when the range of possible keys isn’t huge compared 
to the number of items.


**Put into spot, remove, put back**
This phrase captures the essence of counting sort’s two‐phase approach:
1. **Counting Phase (“put into” the count array):**  
	You create an auxiliary array (the “count” array) whose indices represent each possible key. You then “place” each item by incrementing the count at the index corresponding to its key. (You don’t literally remove items from your original list, but you “account” for them.)
2. **Placing Phase (“remove, put back”):**  
	After counting, you compute a cumulative (or prefix) sum of the counts. This cumulative count tells you exactly where in the output array each key’s block begins and ends (this is what we mean by “ranking the file” or determining the first and last positions for each key). Finally, you iterate over the original array—typically in reverse to preserve stability—and “put back” each element into its correct spot in a new, sorted output array, decrementing the corresponding count as you go.


**Goal is to save record Moves**
By counting the occurrences first and then calculating positions, counting sort minimizes the number of data moves. Instead of repeatedly swapping or shifting records (as happens in many comparison-based sorts), each item is moved exactly once from the input into its final sorted position.

![[Pasted image 20250218041315.png]]


### 4. Dynamic Programming
Runtime of dynamic programming
- O($d^n$)

Principal of Optimality
- At the optimum solution, you can go to any stage i such that, no matter the value of $s_i$ and $d_i$ , the subsequent decisions $d_i+1$, $d_i+2$, ... $d_n$ are optimal.

### 5. Algorithms
Know how to build recurrences based on pseudocode.
- Merge sort
	- merge sort
	- merge sort 
	- merge
- Quicksort
	- partition 
	- quick sort
	- quick sort

### 6. Median of Medians
Derive recurrence relation
- if 7 rows
	- n/7 
	- 10/7
	- Cn + T(n/7) + T(10/14)
- if 9 rows
	- Cn + T(n/9) + T(13n/18)
5 7 9

all odd numbers 5 or greater, linear

Median-of-Medians (Deterministic Linear‑Time Selection)
- **Method:**
    1. **Divide:** Partition the array into ⎡n/r⎤ subarrays of size _r_ (with _r_ typically chosen as 5, which empirical and theoretical analyses suggest is a good constant).
    2. **Conquer Locally:** Find the median of each subarray (which takes constant time per subarray since _r_ is fixed).
    3. **Recursion:** Recursively determine the median of these medians; denote it as _m_.
    4. **Partition:** Use _m_ as a pivot to partition the original array.

### 6. Misc

State and justify your best upper bound on comparison based sorting.
- The best upper bound on comparison-based sorting is O(n log n), justified by the decision tree model: any comparison sort must distinguish between n! possible orderings, requiring at least log₂(n!) = O(n log n) comparisons in the worst case. Merge Sort and Heap Sort achieve this bound, proving it is asymptotically tight.

State and justify your best lower bound on comparison based sorting.
- The best lower bound on comparison-based sorting is Ω(n log n), justified by the decision tree model: since a comparison sort must distinguish between n! possible orderings, the height of the decision tree (representing the worst-case number of comparisons) is at least log₂(n!) = Ω(n log n) by Stirling’s approximation.

What is the largest number of multiplies we could incur when multiplying tow 5x5 matricies and still be faster than Strassen's algorithm?
- Strassen's algorithms is: O($n^{2.81}$) 
- Answer: $O(5^{2.81})$

