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

$T(n) = 7T\left(\frac{n}{2}\right)$ 

Solving this recurrence gives:

which is asymptotically faster than the naive method.