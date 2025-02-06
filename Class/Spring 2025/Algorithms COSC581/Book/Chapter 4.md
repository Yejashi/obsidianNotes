### Divide-and-Conquer Method

The divide-and-conquer method is a powerful strategy for designing asymptotically efficient algorithms. It involves solving a given problem recursively by breaking it into smaller subproblems. If the problem is small enough (base case), it is solved directly without recursion. Otherwise (recursive case), the following three steps are performed:

1. **Divide**: Split the problem into one or more smaller instances of the same problem.
2. **Conquer**: Solve each subproblem recursively.
3. **Combine**: Merge the solutions of the subproblems to form a solution to the original problem.

This recursive breakdown continues until the base case is reached, at which point the recursion bottoms out.

### Recurrences

To analyze recursive divide-and-conquer algorithms, we use **recurrences**—equations that **describe a function in terms of its values on smaller inputs**. Recurrences naturally characterize the running times of recursive algorithms.

Recurrences go hand in hand with the divide-and-conquer method because they give us a natural way to characterize the running times of recursive algorithms mathematically.

The general form of a recurrence is an equation or inequality that describes a function over the integers or reals using the function itself.

A recurrence generally has two or more cases:
- **Base case**: Defines the stopping condition where no recursion is required.
- **Recursive case**: Defines how the function calls itself with smaller arguments.

#### Algorithmic Recurrences
A recurrence $T(n)$ is called **algorithmic** if, for a sufficiently large threshold constant $n_0 > 0$, it satisfies:
1. For all $n < n_0$, we have $T(n) = \Theta(1)$.
2. For all $n \geq n_0$, every recursive call eventually reaches a base case in finite time.

These conditions ensure that the recurrence represents a correct divide-and-conquer algorithm.

#### Conventions for Recurrences
- When a recurrence is stated without an explicit base case, we assume it is algorithmic.
- Asymptotic solutions usually remain unchanged when omitting floors and ceilings.
- If a recurrence is given as an inequality, its solution is expressed using Big-O notation for upper bounds and Omega notation for lower bounds.

### Applications: Matrix Multiplication

We analyze two divide-and-conquer algorithms for multiplying $n \times n$ matrices.
#### Simple Divide-and-Conquer Matrix Multiplication
Section 4.1 presents an algorithm that divides a problem of size $n$ into four subproblems of size $n/2$ which it then solves recursively.

The running time of the algorithm can be characterized by the recurrence:

$T(n) = 8T\left(\frac{n}{2}\right)+ \Theta(1)$  

Which turns out to have the solution :

$T(n) = \Theta(n^3)$  

which is no faster than the naive $O(n^3)$ approach.

Although this divide-and- conquer algorithm is no faster than the straightforward method that uses a triply nested loop, it leads to an asymptotically faster divide-and-conquer algorithm due to V. Strassen, which we’ll explore in Section 4.2.

Strassen’s algorithm improves efficiency by dividing the problem into seven subproblems of size $n/2$:

$T(n) = 7T\left(\frac{n}{2}\right) + \Theta(n^2)$ 

Solving this recurrence gives:
![[Pasted image 20250206050233.png]]

which is asymptotically faster than the naive method.

### Solving Recurrences

After studying matrix multiplication, we explore mathematical tools for solving recurrences. The textbook presents four methods:

1. **Substitution Method (Section 4.3)**: Guess the form of the solution and prove it using mathematical induction.
2. **Recursion-Tree Method (Section 4.4)**: Expand the recurrence into a tree and sum the costs across all levels.
3. **Master Theorem (Section 4.5)**: Provides a direct formula for solving recurrences of the form: $T(n) = aT\frac{n}{b}+ f(n)$ 
4. **Iterative Method (Section 4.6)**: Iteratively expand the recurrence and identify patterns.

Each method has its advantages and is applicable to different types of recurrences.

## 4.1 Matrix Multiplying Matrices

### Matrix Multiplication Using Divide-and-Conquer

#### Introduction

Matrix multiplication is a fundamental operation in computational mathematics. Given two square matrices, we can compute their product using various techniques. This document explores the traditional approach and a divide-and-conquer strategy for matrix multiplication.

### Standard Matrix Multiplication

Let matrices $A = (a_{ik})$ and $B = (b_{kj})$ be square matrices of size $n \times n$. Their product, denoted as $C = A \times B$, is also an $n \times n$ matrix, where each element is computed as:

![[Pasted image 20250206054154.png]]

This formula implies that computing $C$ requires $n^2$ entries, each of which involves the sum of $n$ products from the input matrices.

#### Computational Complexity
The standard approach iterates over three nested loops:

```
MATRIX-MULTIPLY(A, B, C, n)
1. for i = 1 to n:
2.     for j = 1 to n:
3.         for k = 1 to n:
4.             C[i][j] = C[i][j] + A[i][k] * B[k][j]
```

Each iteration of the triply nested loop performs a constant-time operation, leading to an overall time complexity of $\mathcal{O}(n^3)$.

### Divide-and-Conquer Matrix Multiplication
For a more efficient approach, we can use the divide-and-conquer method. This involves partitioning the matrices into smaller submatrices and recursively computing their products.
#### Matrix Partitioning
We divide each matrix into four equal-sized submatrices:
![[Pasted image 20250206054502.png]]

The product can be expressed as:

![[Pasted image 20250206054525.png]]

This method requires eight recursive multiplications and four additions of submatrices of size $n/2 \times n/2$.

#### Implementation Using Recursion
The divide-and-conquer approach can be implemented recursively:

```
MATRIX-MULTIPLY-RECURSIVE(A, B, C, n)
1. if n == 1:
2.     C[1][1] = C[1][1] + A[1][1] * B[1][1]
3.     return
4. Partition A, B, and C into n/2 x n/2 submatrices
5. Recursively compute:
6.     MATRIX-MULTIPLY-RECURSIVE(A11, B11, C11, n/2)
7.     MATRIX-MULTIPLY-RECURSIVE(A11, B12, C12, n/2)
8.     MATRIX-MULTIPLY-RECURSIVE(A21, B11, C21, n/2)
9.     MATRIX-MULTIPLY-RECURSIVE(A21, B12, C22, n/2)
10.    MATRIX-MULTIPLY-RECURSIVE(A12, B21, C11, n/2)
11.    MATRIX-MULTIPLY-RECURSIVE(A12, B22, C12, n/2)
12.    MATRIX-MULTIPLY-RECURSIVE(A22, B21, C21, n/2)
13.    MATRIX-MULTIPLY-RECURSIVE(A22, B22, C22, n/2)
```

### Time Complexity Analysis

Let $T(n)$ represent the worst-case time complexity for multiplying two $n \times n$ matrices recursively. The recurrence relation is:

![[Pasted image 20250206054705.png]]

Using the Master Theorem, we find that:

![[Pasted image 20250206054752.png]]

which is the same as the standard matrix multiplication algorithm. However, further improvements (e.g., Strassen’s algorithm) can reduce this complexity.

### Conclusion

The divide-and-conquer method provides a structured approach to matrix multiplication and lays the groundwork for more efficient algorithms such as Strassen’s method. However, due to the overhead of recursive calls and submatrix partitioning, it does not improve the asymptotic complexity over the naive approach.


## 4.2 Strassen's algorithm for matrix multiplication

Strassen’s algorithm for matrix multiplication is a groundbreaking approach that breaks the conventional $O(n^3)$ barrier for multiplying two $n \times n$ matrices. Traditionally, the natural definition of matrix multiplication requires $n^3$ scalar multiplications. Many believed that an $O(n^3)$ algorithm was optimal until 1969, when V. Strassen introduced a recursive algorithm that achieves a running time of $O(n^{\lg 7})$, which is approximately $O(n^{2.81})$.

### Motivation and Background

- **Traditional Multiplication Complexity:**  
    The straightforward method for matrix multiplication requires $n^3$ scalar multiplications because each element of the result is computed as a sum of $n$ products.
- **The Idea of Reducing Multiplications:**  
    Strassen’s key insight is to reduce the number of recursive multiplications at the expense of performing more additions and subtractions. Although the cost of extra additions is not negligible, it is dominated by the cost of multiplications for large matrices.
- **An Illustrative Algebraic Trick:**  
    Consider two numbers $x$ and $y$ and the desire to compute $x^2 - y^2$. The standard approach would involve two multiplications (one for $x^2$ and one for $y^2$) and one subtraction. 
	
	However, by rewriting the expression as  :
	
    $x^2 - y^2 = (x+y)(x-y)$ 

    one multiplication and two additions (or a subtraction, which is similar to addition with a sign change) suffice. Although the saving is marginal for scalars, the advantage grows for large matrices.

### Divide-and-Conquer Strategy

Strassen’s algorithm uses the divide-and-conquer method, similar to the approach in the standard recursive matrix multiplication algorithm (often called MATRIX-MULTIPLY-RECURSIVE), but it strategically reduces the number of recursive multiplications:

- **Partitioning:**  
    Given three $n \times n$ matrices $A$, $B$, and $C$ (with $C = A \times B$), where $n$ is an exact power of 2, the matrices are partitioned into four submatrices of size $\frac{n}{2} \times \frac{n}{2}$.
    
- **Reduction in Multiplications:**  
    Instead of performing eight multiplications on these submatrices, Strassen’s algorithm cleverly computes only seven multiplications and uses additional matrix additions and subtractions (which are less costly) to combine the results.
    
- **Recurrence Relation:**  
    The algorithm’s running time is captured by the recurrence :
     $T(n) = 7T\left(\frac{n}{2}\right) + \Theta(n^2)$
    By applying the master theorem, this recurrence solves to :
    $T(n) = \Theta(n^{\lg 7}) \approx O(n^{2.81})$
    which is an asymptotic improvement over the traditional $O(n^3)$ method.

### Detailed Algorithm Steps

The algorithm proceeds in four main steps:

### Step 1: Base Case and Partitioning
- **Base Case:**  
    If $n = 1$, each matrix has a single element. The algorithm performs one scalar multiplication and one scalar addition (as in the MATRIX-MULTIPLY-RECURSIVE algorithm) in constant time, denoted as $\Theta(1)$.
    
- **Partitioning:**  
    For $n > 1$, the input matrices $A$, $B$, and the output matrix $C$ are partitioned into four submatrices of size $\frac{n}{2} \times \frac{n}{2}$, as described by the standard partitioning equation.

### Step 2: Creating Auxiliary Matrices
- **Matrix Creation:**  
    Create 10 auxiliary matrices, $S_1, S_2, \ldots, S_{10}$, where each $S_i$ is defined as the sum or difference of two of the submatrices from the partitioned matrices. For example:
    
    - $S_1 = B_{12} - B_{22}$
    - $S_2 = A_{11} + A_{12}$
    - $S_3 = A_{21} + A_{22}$
    - $S_4 = B_{21} - B_{11}$
    - $S_5 = A_{11} + A_{22}$
    - $S_6 = B_{11} + B_{22}$
    - $S_7 = A_{12} - A_{22}$
    - $S_8 = B_{21} + B_{22}$
    - $S_9 = A_{11} - A_{21}$
    - $S_{10} = B_{11} + B_{12}$
- **Initialization of Product Matrices:**  
	Additionally, create seven matrices $P_1, P_2, \ldots, P_7$ (initialized to zero) to hold the results of the seven recursive multiplications. The creation and initialization of these 17 matrices require $\Theta(n^2)$ time.

### Step 3: Recursive Multiplications
Using the submatrices from the partitioning step and the $S_i$ matrices, compute the following seven products recursively (each product involves multiplying two $\frac{n}{2} \times \frac{n}{2}$ matrices):

- $P_1 = A_{11} \times S_1$, which represents $A_{11} \times (B_{12} - B_{22})$
- $P_2 = S_2 \times B_{22}$, which represents $(A_{11} + A_{12}) \times B_{22}$
- $P_3 = S_3 \times B_{11}$, which represents $(A_{21} + A_{22}) \times B_{11}$
- $P_4 = A_{22} \times S_4$, which represents $A_{22} \times (B_{21} - B_{11})$
- $P_5 = S_5 \times S_6$, which represents $(A_{11} + A_{22}) \times (B_{11} + B_{22})$
- $P_6 = S_7 \times S_8$, which represents $(A_{12} - A_{22}) \times (B_{21} + B_{22})$
- $P_7 = S_9 \times S_{10}$, which represents $(A_{11} - A_{21}) \times (B_{11} + B_{12})$

This step takes $7T\left(\frac{n}{2}\right)$ time.

### Step 4: Combining the Products to Form the Final Matrix
Update the four submatrices of $C$ using the computed $P_i$ matrices with additions and subtractions (each update takes $\Theta(n^2)$ time):

Overall, Step 4 involves 12 additions or subtractions of $\frac{n}{2} \times \frac{n}{2}$ matrices, which again takes $\Theta(n^2)$ time.
### Recurrence Analysis and Conclusion
By combining the costs of all steps:
- **Base Case:** $\Theta(1)$ time.
- **Partitioning, Creation, and Combining:** $\Theta(n^2)$ time.
- **Recursive Multiplications:** $7T\left(\frac{n}{2}\right)$ time.

This gives the recurrence relation:  

$T(n) = 7T\left(\frac{n}{2}\right) + \Theta(n^2)$

Using the master theorem, the solution to this recurrence is:  

$T(n) = \Theta(n^{\lg 7}) \approx O(n^{2.81})$

Thus, Strassen’s algorithm asymptotically outperforms the standard $O(n^3)$ matrix multiplication algorithms by reducing the number of multiplications required at each recursive step, even though it increases the number of additions. This trade-off is highly beneficial for large matrices where multiplication dominates the running time.

### Summary

Strassen’s algorithm is a seminal divide-and-conquer method that:
- Reduces the number of recursive multiplications from 8 to 7.
- Introduces 10 auxiliary matrices for sums and differences.
- Combines the seven computed products to form the final matrix.
- Achieves a running time of $O(n^{2.81})$, thereby beating the conventional $O(n^3)$ methods.

## 4.3 The substitution method for solving recurrences

The substitution method is a general technique used to solve recurrences—equations that characterize the running times of divide-and-conquer algorithms. It consists of two main steps:

1. **Guess the Form of the Solution:**  
    Formulate a guess using symbolic constants.
2. **Prove the Guess by Induction:**  
    Use mathematical induction to verify that the solution works and determine the constants.

This method is called the _substitution method_ because you substitute your guessed solution into the recurrence for smaller inputs as part of the inductive step.

### Using the Substitution Method to Establish Bounds

The substitution method can be used to establish either an upper bound or a lower bound for a recurrence. It is generally advisable to prove one bound at a time. For instance, you might first prove an $O$-bound and then prove an $\Omega$-bound; together, these yield a $\Theta$-bound (as seen in Theorem 3.1 in the textbook).

### Example: An Asymptotic Upper Bound

Consider the recurrence

$T(n) = 2\, T\!\left(\frac{n}{2}\right) + \Theta(n)$

This recurrence is similar to that for merge sort (with the floor function ensuring $T(n)$ is defined on the integers). We guess that:

$T(n)=O(nlogn)$

and then use the substitution method to prove this bound.

#### Inductive Hypothesis

We assume that for all $n \ge n_0$ (for some constant $n_0 > 0$), the following holds:

$T(n) \le c\, n \log n$

where $c > 0$ is a constant to be determined.

_Note:_ It is crucial **not** to use asymptotic notation (like $O(n \lg n)$) directly in the inductive hypothesis because the hidden constants can differ from one step to another.

#### Inductive Step

1. **Assumption for Smaller Values:**  
    Assume the hypothesis holds for all values smaller than $n$. In particular, for $n \ge 2n_0$, it holds for $\lfloor n/2 \rfloor$:
		$T(⌊n/2⌋)≤c⌊n/2⌋log⌊n/2⌋.$
2. **Substitution into the Recurrence:**  
	Substitute the hypothesis into the recurrence:
		![[Pasted image 20250206061901.png]]

	To conclude that
		![[Pasted image 20250206062013.png]]
	 we choose $c$ and $n_0$ sufficiently large such that the term $\Theta(n)$ is dominated by the $c, n$ term.

#### Base Case

For the base cases (when $n_0 \le n < 2n_0$), the recurrence is defined as algorithmic (i.e., $T(n)$ is constant for these small values). By picking a specific $n_0$ (say, $n_0 = 2$) and choosing

![[Pasted image 20250206062126.png]]
we ensure that:

![[Pasted image 20250206062147.png]]

Thus, the inductive hypothesis holds for all $n \ge 2$, implying:

![[Pasted image 20250206062211.png]]

### Making a Good Guess

There is no general method to correctly guess the tightest asymptotic solution for an arbitrary recurrence. Good guesses are developed through experience, practice, and sometimes creativity. Some techniques include:

- **Recurrence-Solving Heuristics:**  
    Familiarity with common recurrences can lead to reasonable guesses.
    
- **Recursion Trees:**  
    These help visualize the recurrence and guide your guess.
    
- **Comparing with Known Recurrences:**  
    If the recurrence resembles a known one (for example, merge sort), a similar solution may be a good starting point.

For example, consider the recurrence:

![[Pasted image 20250206062254.png]]
which is similar to merge sort despite the $+17$ term. Intuitively, when $n$ is large, the $+17$ is insignificant, so one can guess $T(n) = O(n \lg n)$ and verify it using the substitution method.

Another approach is to first establish loose upper and lower bounds and then narrow the gap until the tight solution is identified.


### A Trick of the Trade: Subtracting a Lower-Order Term

Sometimes your initial guess is nearly correct, but the induction does not work out because the inductive hypothesis is not strong enough. In such cases, **subtracting a lower-order term** from your guess can strengthen the hypothesis.

#### Example

Consider the recurrence

![[Pasted image 20250206062416.png]]

and suppose we guess $T(n) = O(n)$. A naive induction might set

![[Pasted image 20250206062440.png]]

but substitution yields

![[Pasted image 20250206062503.png]]

which does not immediately imply $T(n) \le c, n$ because of the extra constant. Instead, try a stronger hypothesis:

![[Pasted image 20250206062529.png]]

where $d \ge 0$ is a constant. Substituting this into the recurrence gives:

![[Pasted image 20250206062545.png]]

By choosing $d$ large enough (to counteract the $\Theta(1)$ term), you can complete the induction. This subtraction effectively cancels out the extra lower-order terms introduced by multiple recursive calls.

### Summary

- **Substitution Method Overview:**  
    Guess the solution, then use induction to prove it.
    
- **Proving Bounds:**  
    Prove either an upper or lower bound first by making an inductive hypothesis with explicit constants.
    
- **Making a Good Guess:**  
    Use intuition, experience, and tools like recursion trees.
    
- **Strengthening the Inductive Hypothesis:**  
    If necessary, subtract a lower-order term to handle extra constant terms.
    
- **Avoiding Pitfalls:**  
    Always be precise with constants and avoid using loose asymptotic notation in your hypothesis.