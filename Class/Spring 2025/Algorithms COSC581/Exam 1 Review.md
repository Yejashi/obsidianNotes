
### 1. Asymptotics
L'hopitals Rule
> derivative of a log

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

### 3. Sorting
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