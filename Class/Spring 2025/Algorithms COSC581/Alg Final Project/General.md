### **What Are We Trying to Do?**

We have some **input variables** (e.g., problem size, number of threads) and a **performance measurement** (e.g., runtime). Our goal is to **find a polynomial function** that best predicts the performance based on these inputs.

### **Step 1: Writing the Polynomial Equation**

Let's say we have two input variables:

- x (e.g., number of threads)
- y (e.g., problem size)

A polynomial equation that models performance (zzz) could look like this:

z=β1+β2x+β3y+β4x2+β5xy+β6y2z = \beta_1 + \beta_2 x + \beta_3 y + \beta_4 x^2 + \beta_5 xy + \beta_6 y^2z=β1​+β2​x+β3​y+β4​x2+β5​xy+β6​y2

- The β\betaβ values (coefficients) are **unknown** and need to be solved for.
- The terms like x2x^2x2, xyxyxy, and y2y^2y2 capture **nonlinear effects**.

### **Step 2: Representing the Data in a Matrix**

Imagine we collect several observations. Each row represents one observation, where we record xxx, yyy, and the actual measured zzz (performance).

For three data points:

|xxx|yyy|zzz (measured)|
|---|---|---|
|1|2|5|
|2|3|8|
|3|4|12|

Now, for each row, we write out the polynomial terms:

|1 (constant)|xxx|yyy|x2x^2x2|xyxyxy|y2y^2y2|zzz|
|---|---|---|---|---|---|---|
|1|1|2|1|2|4|5|
|1|2|3|4|6|9|8|
|1|3|4|9|12|16|12|

This matrix is called **XXX**:

X=[11212412346913491216]X = \begin{bmatrix} 1 & 1 & 2 & 1 & 2 & 4 \\ 1 & 2 & 3 & 4 & 6 & 9 \\ 1 & 3 & 4 & 9 & 12 & 16 \end{bmatrix}X=