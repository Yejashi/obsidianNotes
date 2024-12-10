

# Exam 3

**Convoy**:  Set of vector instructions that could potentially execute
together

**Chaining:** Allows a vector operation to start as soon as the individual
elements of its vector source operands become available

**Chime:** Unit of time to execute one convoy
- For vector length of n, requires m x n clock cycles

A **lane** is a sub-unit within a vector processing unit that can execute operations on one element of a vector.

##### What is Strip Mining?
When a loop processes a dataset that is too large for a vector processing unit, strip mining splits the loop iteration space into smaller "strips" that fit the hardware's processing capacity. 

It divides a large problem into smaller chunks, or "strips," which are processed sequentially, but within each strip, work is vectorized.

##### What is a vector mask register?

Vector mask registers are special registers which control which elements in a vector operation are active.

Each bit in the mask corresponds to a vector element, with 1 enabling execution for that element and 0 disabling it.

They are used for handling if statements in vector loops.

Purpose:
- 


