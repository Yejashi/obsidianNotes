### **What Are We Trying to Do?**

We have some **input variables** (e.g., problem size, number of threads) and a **performance measurement** (e.g., runtime). Our goal is to **find a polynomial function** that best predicts the performance based on these inputs.

### **Step 1: Writing the Polynomial Equation**

Let's say we have two input variables:

- x (e.g., number of threads)
- y (e.g., problem size)

A polynomial equation that models performance (z) could look like this:

$z = \beta_1 + \beta_2 x + \beta_3 y + \beta_4 x^2 + \beta_5 xy + \beta_6 y^2$

- The β values (coefficients) are **unknown** and need to be solved for.
- The terms like $x^2$, xy, and $y^2$ capture **nonlinear effects**.

### **Step 2: Representing the Data in a Matrix**

Imagine we collect several observations. Each row represents one observation, where we record x, y, and the actual measured z (performance).

For three data points:

| x   | y   | z (measured) |
| --- | --- | ------------ |
| 1   | 2   | 5            |
| 2   | 3   | 8            |
| 3   | 4   | 12           |

Now, for each row, we write out the polynomial terms:

| 1 (constant) | x   | y   | $x^2$ | xy  | $y^2$ | z   |
| ------------ | --- | --- | ----- | --- | ----- | --- |
| 1            | 1   | 2   | 1     | 2   | 4     | 5   |
| 1            | 2   | 3   | 4     | 6   | 9     | 8   |
| 1            | 3   | 4   | 9     | 12  | 16    | 12  |

This matrix is called **X**:

$X = \begin{bmatrix} 1 & 1 & 2 & 1 & 2 & 4 \\ 1 & 2 & 3 & 4 & 6 & 9 \\ 1 & 3 & 4 & 9 & 12 & 16 \end{bmatrix}$

And our target **Z** (measured performance values) is:

$Z = \begin{bmatrix} 5 \\ 8 \\ 12 \end{bmatrix}$

Our unknowns (β\betaβ) are:

$\beta = \begin{bmatrix} \beta_1 \\ \beta_2 \\ \beta_3 \\ \beta_4 \\ \beta_5 \\ \beta_6 \end{bmatrix}$

### **Step 3: Solving for β Using Least Squares**

We need to find β that best fits the equation:

$X \beta = Z$

Since we may not have an exact solution, we solve **the least squares problem**:

(XTX)β=XTZ(X^T X) \beta = X^T Z(XTX)β=XTZ

We solve this system using methods like **LU decomposition** or **QR decomposition**, which are just ways to efficiently compute β\betaβ.