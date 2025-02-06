### Divide-and-Conquer Method

The divide-and-conquer method is a powerful strategy for designing asymptotically efficient algorithms. It involves solving a given problem recursively by breaking it into smaller subproblems. If the problem is small enough (base case), it is solved directly without recursion. Otherwise (recursive case), the following three steps are performed:

1. **Divide**: Split the problem into one or more smaller instances of the same problem.
2. **Conquer**: Solve each subproblem recursively.
3. **Combine**: Merge the solutions of the subproblems to form a solution to the original problem.

This recursive breakdown continues until the base case is reached, at which point the recursion bottoms out.

### Recurrences

To analyze recursive divide-and-conquer algorithms, we use **recurrences**—equations that **describe a function in terms of its values on smaller inputs**. Recurrences naturally characterize the running times of recursive algorithms.

A recurrence generally has two or more cases:
- **Base case**: Defines the stopping condition where no recursion is required.
- **Recursive case**: Defines how the function calls itself with smaller arguments.

For example, the recurrence for merge sort is given in Section 2.3.2 of _Introduction to Algorithms_.
#### Algorithmic Recurrences
A recurrence $T(n)$ is called **algorithmic** if, for a sufficiently large threshold constant $n_0 > 0$, it satisfies:
1. For all $n < n_0$, we have $T(n) = \Theta(1)$.
2. For all $n \geq n_0$, every recursive call eventually reaches a base case in finite time.