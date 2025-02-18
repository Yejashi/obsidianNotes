
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

example of case 3
- f(n) = 2T($n/2$) + $\Theta(n^2)$ 
- a = 2 
- b = 2
- f(n) = n^2
- n^logb1 = n
- lim n^2/n^

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
		
	**Case 2:**
		$T(n) = 16T(\frac{n}{4}) + n^2$ 
		a = 16 b = 4 f(n) = $n^2$ 
		$n^{log_{4}16}$ = $n^2$
		$f(n) = \Theta(n^2)$ 
		lim $n^2/n^2$ = 1 does not equal $\infty, 0$ 

### 3. Sorting

| Algorithm                         | Key Comparisons  | Record Moves   | Extra Space | Stability | Simplicity | Best Case | Average Case |
|----------------------------------|------------------|----------------|-------------|-----------|------------|------------|--------------|
| **Bubble Sort**                  | O($n^2$)        | O($n^2$)       | No          | Yes       | Very       | O($n$)     | ?            |
| **Insertion Sort (Straight)**     | O($n^2$)        | O($n^2$)       | No          | Yes       | Very       | O($n$)     | ?            |
| **Insertion Sort (Binary, Huge Files)** | O($n\log n$) | O($n^2$)       | No          | Yes       | Yes-ish    | O($n$)     | O($n\log n$) |
| **Counting Sort** (Knuth’s version) | O($n^2$)      | O($n$)         | Yes         | Yes       | Yes        | O($n^2$)   | O($n^2$)     |
| **Shell Sort (Diminishing Increment)** | O($n^{1.5}$) | ?              | No          | No        | No         | ?          | ?            |
| **Merge Sort**                    | O($n\log n$)    | O($n\log n$)   | Yes         | Yes       | Yes        | O($n\log n$) | O($n\log n$) |
| **Heap Sort**                     | O($n\log n$)    | O($n\log n$)   | No          | No        | Not really | O($n\log n$) | O($n\log n$) |
| **Quick Sort**                    | O($n^2$)        | O($n^2$)       | No          | No        | No         | O($n\log n$) | ?            |
| **Radix Sort**                    | O($$)        | O($$)       | No          | No        | No         | O($$) | ?            |
| **Bucket Sort**                    | O($$)        | O($$)       | No          | No        | No         | O($$) | ?            |
- Know the table
- Call sequences for recursive ones
	- Merge sort
	- Heap sort (build the heap)

Count sort
- List of 5 items
- put into spot, remove, put back
- goal is to save record moves 
- Origninal counting sourt as done by DOn Kenith
- first and last (ranking the file)

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


Look at Langston's website