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



## 3.2 Asymptotic notation: formal definitions

### Asymptotic Notations: O, Ω, and Θ

Asymptotic notation is used to characterize the running time of algorithms. It provides a way to express the growth rates of functions, specifically how they behave as the input size increases. The main notations used are **O (Big-O)**, **Ω (Big-Omega)**, and **Θ (Big-Theta)**.

#### O-Notation: Upper Bound

- **Definition**: O-notation provides an upper bound on a function, indicating that a function's growth will never exceed a certain rate, up to a constant factor. If $f(n) = O(g(n))$, this means that there exist constants $n_0$ and $c$ such that for all $n \geq n_0$, $f(n) \leq c \cdot g(n)$.
    
- **Intuition**: The function $f(n)$ lies at or below a constant multiple of $g(n)$ for sufficiently large $n$. This is useful for analyzing the worst-case behavior of algorithms.
    
- **Example**: For $f(n) = 4n^2 + 100n + 500$, we can show that $f(n) = O(n^2)$ because, for sufficiently large $n$, the $n^2$ term dominates. By choosing appropriate constants $c$ and $n_0$, we can bound $f(n)$ by $c \cdot n^2$.
    
    - For example, if $n_0 = 1$, $c = 604$ works; if $n_0 = 10$, $c = 19$ works.
- **Key Point**: The definition of $O(g(n))$ requires that $f(n)$ is asymptotically nonnegative, meaning it must be nonnegative for sufficiently large $n$.
    

#### Ω-Notation: Lower Bound

- **Definition**: Ω-notation provides a lower bound for a function, meaning that the function's growth rate is at least as fast as $g(n)$, up to a constant factor. If $f(n) = \Omega(g(n))$, then there exist constants $n_0$ and $c$ such that for all $n \geq n_0$, $f(n) \geq c \cdot g(n)$.
    
- **Intuition**: For sufficiently large $n$, the function $f(n)$ is on or above a constant multiple of $g(n)$.
    
- **Example**: For $f(n) = 4n^2 + 100n + 500$, we can show that $f(n) = \Omega(n^2)$ by choosing $n_0$ and $c$ appropriately. For instance, dividing by $n^2$ gives $4 + 100/n + 500/n^2 \geq c$. This holds for $c = 4$ and any positive $n_0$.
    

#### Θ-Notation: Tight Bound

- **Definition**: Θ-notation is used to describe an asymptotically tight bound. If $f(n) = \Theta(g(n))$, then there exist constants $n_0$, $c_1$, and $c_2$ such that for all $n \geq n_0$, $c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)$.
    
- **Intuition**: The function $f(n)$ lies between two constant multiples of $g(n)$ for sufficiently large $n$. It’s a more precise description of an algorithm's running time compared to $O$ and $\Omega$.
    
- **Example**: For $f(n) = 4n^2 + 100n + 500$, we can say that $f(n) = \Theta(n^2)$ because both an upper and lower bound can be found for $n \geq n_0$.
    

#### Theorem 3.1: Relationship Between Notations

For two functions $f(n)$ and $g(n)$, we have:

$f(n) = \Theta(g(n))$ if and only if $f(n) = O(g(n))$ and $f(n) = \Omega(g(n))$

This theorem helps in proving tight bounds by combining upper and lower bounds.

---

### Applying Asymptotic Notation to Running Times

When characterizing an algorithm's running time, it’s important to choose the most precise asymptotic notation. Here are some examples:

- **Insertion Sort**:
    
    - **Worst-case**: $O(n^2)$, $\Omega(n^2)$, and $\Theta(n^2)$.
    - **Best-case**: $O(n)$, $\Omega(n)$, and $\Theta(n)$.
    
    The **$\Theta(n^2)$** bound is the most precise for the worst case, while **$\Theta(n)$** is the most precise for the best case.
    
- **Merge Sort**:
    
    - The running time is $\Theta(n \log n)$ in all cases, so it’s sufficient to just say $\Theta(n \log n)$.

#### Common Mistakes

- Confusing $O$-notation with $\Theta$-notation: $O(n^2)$ indicates only an upper bound, not a tight bound. For example, saying "an $O(n \log n)$-time algorithm runs faster than an $O(n^2)$-time algorithm" is incorrect, as the $O(n^2)$ algorithm might actually run faster in practice.
    
- Incorrectly stating that a running time is $\Theta(n^2)$ when it’s not always the worst-case time complexity. For example, insertion sort's running time is $O(n^2)$ but not $\Theta(n^2)$ in all cases.
    

### Using Asymptotic Notation in Equations

Asymptotic notation is often used in equations to express an anonymous function's growth rate. For example:

- $4n2+100n+500=O(n2)4n^2 + 100n + 500 = O(n^2)4n2+100n+500=O(n2)$
    
- $2n2+3n+1=2n2+Θ(n)2n^2 + 3n + 1 = 2n^2 + \Theta(n)2n2+3n+1=2n2+Θ(n)$
    

In these cases, the asymptotic notation stands for some function whose exact form we don’t need to specify. This simplifies the equation by focusing only on the dominant term, making it easier to analyze and compare the growth rates of different functions.

### Summary

- **O-notation**: Provides an upper bound on the growth rate.
- **Ω-notation**: Provides a lower bound on the growth rate.
- **Θ-notation**: Provides a tight, asymptotic bound.
- Choose the most precise notation possible to avoid overstating or understating the algorithm’s running time.