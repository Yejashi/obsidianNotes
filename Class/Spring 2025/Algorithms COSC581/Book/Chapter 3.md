## 3.1 O-notation, Omega notation, theta notation

### Asymptotic Notation in Algorithm Analysis

Asymptotic notation is a way to characterize the running times of algorithms in terms of how they scale with input size. It helps us focus on the dominant terms and ignore less significant details. In this section, we explore different forms of asymptotic notation, including O-notation, Ω-notation, and Θ-notation, using insertion sort as an example.

---

### O-Notation (Upper Bound)

O-notation is used to describe an upper bound on the asymptotic behavior of a function. It characterizes the worst-case scenario of an algorithm’s running time, ensuring that the function does not grow faster than a certain rate.

- Example: Consider the function $7n^3 + 100n^2 - 20n + 6$. The highest-order term is $7n^3$, so we say that the function grows no faster than $n^3$. Therefore, we can write it as $O(n^3)$.
- It is also true that this function can be written as $O(n^4)$, $O(n^5)$, and so on, because the function grows slower than these terms.

### Ω-Notation (Lower Bound)

Ω-notation characterizes a lower bound on the asymptotic behavior of a function. It states that the function grows at least as fast as a certain rate based on the highest-order term.

- For the function $7n^3 + 100n^2 - 20n + 6$, since the highest-order term $n^3$ grows at least as fast as $n^3$, we can say that the function is $\Omega(n^3)$.
- This function is also $\Omega(n^2)$ and $\Omega(n)$.

### Θ-Notation (Tight Bound)

Θ-notation provides a tight bound on the asymptotic behavior of a function, stating that it grows precisely at a certain rate. It characterizes the function’s rate of growth within constant factors both from above and below.

- If we can show that a function is both $O(f(n))$ and $\Omega(f(n))$ for some function $f(n)$, then we can conclude that the function is $\Theta(f(n))$.

For example, since the function $7n^3 + 100n^2 - 20n + 6$ is both $O(n^3)$ and $\Omega(n^3)$, we can say that it is $\Theta(n^3)$.

---

### Example: Insertion Sort

To understand how asymptotic notation is applied in practice, let’s revisit the insertion sort algorithm and analyze its running time.

#### Insertion Sort Algorithm

```cpp
INSERTION-SORT(A, n):
    for i = 2 to n:
        key = A[i]
        j = i - 1
        while j > 0 and A[j] > key:
            A[j + 1] = A[j]
            j = j - 1
        A[j + 1] = key

```

The algorithm consists of two nested loops:

1. **Outer Loop:** This loop runs $n-1$ times, regardless of the input.
2. **Inner Loop:** This loop's iterations depend on the values being sorted. It may run anywhere from 0 to $i-1$ times for each iteration of the outer loop.

#### Worst-Case Running Time

- **O-Notation (Upper Bound):** The outer loop runs $n-1$ times. The inner loop runs at most $i-1$ times in the $i^{th}$ iteration of the outer loop. Hence, the total number of iterations of the inner loop is at most $(n-1)(n-1)$, which is $O(n^2)$.
    
- **Ω-Notation (Lower Bound):** The worst-case scenario occurs when the array is in reverse order. In this case, each element must be moved to the front, meaning that for every element, the inner loop executes the maximum number of times. Therefore, the running time in the worst case is at least $\Omega(n^2)$.
    
- **Θ-Notation (Tight Bound):** Since we have shown that the running time is both $O(n^2)$ and $\Omega(n^2)$, we can conclude that the worst-case running time is $\Theta(n^2)$.
    

#### Worst-Case Example with Insertion Sort

To illustrate the worst-case scenario, assume that the first $n/3$ positions contain the $n/3$ largest values. These values need to be moved through the middle $n/3$ positions to the last $n/3$ positions, requiring at least $n^2/9$ operations. Therefore, the worst-case time complexity is $\Omega(n^2)$.

---

### Summary of Asymptotic Notations

1. **O-Notation ($O$):** Upper bound on the growth of a function.
2. **Ω-Notation ($\Omega$):** Lower bound on the growth of a function.
3. **Θ-Notation ($\Theta$):** Tight bound on the growth of a function, providing an exact characterization.

In conclusion, asymptotic notations allow us to focus on the dominant terms in an algorithm's running time, simplifying our analysis and understanding of its performance.


