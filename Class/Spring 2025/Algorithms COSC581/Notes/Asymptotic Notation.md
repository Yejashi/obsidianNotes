### 1. **Why Asymptotic Notation?**

In computer science, we often want to analyze the efficiency of algorithms. Specifically, we care about how their running time (or space usage) grows as the input size (nnn) increases.

- Example: Suppose we have two sorting algorithms:
    - Algorithm A takes f(n)=n2f(n) = n^2f(n)=n2 operations.
    - Algorithm B takes g(n)=nlog⁡ng(n) = n \log ng(n)=nlogn operations.
    - If n=10n = 10n=10, then f(10)=100f(10) = 100f(10)=100 and g(10)≈33g(10) \approx 33g(10)≈33.
    - If n=1000n = 1000n=1000, then f(1000)=1,000,000f(1000) = 1,000,000f(1000)=1,000,000 and g(1000)≈10,000g(1000) \approx 10,000g(1000)≈10,000.

Even though the difference wasn't large for small nnn, as nnn grows, g(n)g(n)g(n) is much more efficient than f(n)f(n)f(n). Asymptotic notation helps us compare these growth rates formally.