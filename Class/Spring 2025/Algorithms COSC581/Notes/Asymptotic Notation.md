### 1. **Why Asymptotic Notation?**

![[Pasted image 20250130114230.png]]

### 2. **Growth Rate of Functions**

Before understanding asymptotic notation, you need to recognize common functions used to describe algorithm complexity, ordered from slowest to fastest growth:

1. **Constant**: f(n)=1f(n) = 1f(n)=1 (Example: accessing an element in an array)
2. **Logarithmic**: f(n)=log⁡nf(n) = \log nf(n)=logn (Example: binary search)
3. **Linear**: f(n)=nf(n) = nf(n)=n (Example: looping through an array)
4. **Log-linear**: f(n)=nlog⁡nf(n) = n \log nf(n)=nlogn (Example: efficient sorting algorithms like Merge Sort)
5. **Quadratic**: f(n)=n2f(n) = n^2f(n)=n2 (Example: naive sorting algorithms like Bubble Sort)
6. **Cubic**: f(n)=n3f(n) = n^3f(n)=n3 (Example: matrix multiplication)
7. **Exponential**: f(n)=2nf(n) = 2^nf(n)=2n (Example: brute-force solutions to some NP problems)
8. **Factorial**: f(n)=n!f(n) = n!f(n)=n! (Example: solving Traveling Salesman problem with brute-force)

We use asymptotic notation to categorize these functions and describe how one function compares to another.

