## 3.1 O-notation, Omega notation, theta notation

### Asymptotic Notation and Algorithm Analysis

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