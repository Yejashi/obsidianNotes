
### 1. Asymptotics
L'hopitals Rule
> derivative of a log


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