## 3.1 O-notation, Omega notation, theta notation

### Asymptotic Notation and Algorithm Analysis

In this section, we introduce the different forms of asymptotic notation used to analyze the running time of algorithms, starting with a review of insertion sort. These notations allow us to focus on the rate of growth of the running time while discarding lower-order terms and constant factors.

---

### Insertion Sort Recap

Previously, when analyzing the worst-case running time of insertion sort, we started with a complicated expression and simplified it by discarding lower-order terms and focusing on the leading term. The process of simplifying the expression leads us to represent the running time using **Big-O notation** (denoted as `O(n^2)` for insertion sort’s worst case). This simplified expression focuses on the growth rate of the running time, allowing us to discard coefficients and lower-order terms.

### Key Asymptotic Notations

Asymptotic notation is used to describe the behavior of functions as they grow, and can be applied not only to algorithm running times but also to other aspects like space usage. Below are three common types of asymptotic notation:

#### O-notation (Upper Bound)

**O-notation** describes an upper bound on the growth rate of a function. It tells us that a function grows no faster than a given rate.

Example:

- For the function `7n^3 + 100n^2 - 20n + 6`, the highest-order term is `7n^3`, so we say this function is `O(n^3)`. It is also technically `O(n^4)`, `O(n^5)`, and so on because the function grows more slowly than these terms.

Formally, for any function `f(n)`, if there exist constants `c > 0` and `n_0` such that: $$f(n)≤c⋅g(n)for alln≥n0f(n) \leq c \cdot g(n) \quad \text{for all} \quad n \geq n_0f(n)≤c⋅g(n)for alln≥n0​ then we write `f(n) = O(g(n))`.  



#### Omega-notation (Lower Bound)

**Omega-notation** describes a lower bound on the growth rate of a function. It tells us that a function grows at least as fast as a given rate.

Example:

- For the same function `7n^3 + 100n^2 - 20n + 6`, since the highest-order term `n^3` grows at least as fast as `n^3`, the function is `Ω(n^3)`.

Formally, for any function `f(n)`, if there exist constants `c > 0` and `n_0` such that: f(n)≥c⋅g(n)for alln≥n0f(n) \geq c \cdot g(n) \quad \text{for all} \quad n \geq n_0f(n)≥c⋅g(n)for alln≥n0​ then we write `f(n) = Ω(g(n))`.

#### Theta-notation (Tight Bound)

**Theta-notation** provides a **tight bound**, meaning it describes the rate of growth of a function within a constant factor from above and below. This implies that the function grows at exactly the given rate for large `n`.

Example:

- For the function `7n^3 + 100n^2 - 20n + 6`, we say the function is `Θ(n^3)` because it is both `O(n^3)` and `Ω(n^3)`.

Formally, for any function `f(n)`, if there exist constants `c1 > 0`, `c2 > 0`, and `n_0` such that: c1⋅g(n)≤f(n)≤c2⋅g(n)for alln≥n0c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n) \quad \text{for all} \quad n \geq n_0c1​⋅g(n)≤f(n)≤c2​⋅g(n)for alln≥n0​ then we write `f(n) = Θ(g(n))`.

---

### Applying Asymptotic Notation to Insertion Sort

#### Worst-Case Analysis of Insertion Sort

The insertion sort algorithm is analyzed by examining its nested loops, where the outer loop runs `n-1` times, and the inner loop’s iterations depend on the values being sorted. The worst-case time complexity occurs when the values are in reverse order, meaning the inner loop will execute at its maximum.

The total number of iterations for insertion sort is dominated by the inner loop, leading to a worst-case running time of `O(n^2)`.

Additionally, we can observe that the worst-case running time is **Ω(n^2)** because, in the worst case, each element must be moved to the right, which takes at least `n^2` time.

Thus, the worst-case running time is also **Θ(n^2)**, meaning the time complexity is tightly bound to `n^2` in all cases.

---

### Conclusion

Asymptotic notations, such as `O`, `Ω`, and `Θ`, are essential tools for characterizing the efficiency of algorithms. By focusing on the highest-order terms and ignoring constants and lower-order terms, we can analyze the behavior of algorithms in a manner that is independent of machine specifics, providing general insights into their scalability. The worst-case running time of insertion sort, for example, is `Θ(n^2)`, which tells us that, regardless of the specific input, the time required to sort will grow quadratically as the input size increases.