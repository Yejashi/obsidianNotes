

# Exam 3

**Convoy**:  Set of vector instructions that could potentially execute
together

**Chaining:** Allows a vector operation to start as soon as the individual
elements of its vector source operands become available

**Chime:** Unit of time to execute one convoy
- For vector length of n, requires m x n clock cycles

A **lane** is a sub-unit within a vector processing unit that can execute operations on one element of a vector.

#### What is Strip Mining?
When a loop processes a dataset that is too large for a vector processing unit, strip mining **splits the loop iteration space into smaller "strips" that fit the hardware's processing capacity**. 

It **divides a large problem into smaller chunks**, or "strips," which are **processed sequentially**, but **within each strip, work is vectorized**.

#### What is a vector mask register?

Vector mask registers are special registers which control which elements in a vector operation are active.

Each bit in the mask corresponds to a vector element, with 1 enabling execution for that element and 0 disabling it.

They are used for handling if statements in vector loops.

Purpose:
- Vector mask registers enable conditional execution within vectorized operations, allowing selective computation on specific elements.

TLDR:
- **Vector mask registers control which elements in a vector operation are active.** 
- **They are used for handling if statements in vector loops.**
- **They enable conditional execution within vectorized operations.**

#### Cache Coherence
**Snoopy** and **Directory-based** **protocols** are two types of **cache coherence protocols** used in multiprocessor systems to ensure that multiple caches maintain a consistent view of memory.

##### Snoopy Protocols
In snoopy protocols, all caches in the system watch (or "snoop") the bus to monitor memory transactions (reads/writes) by other processors. The goal is to ensure that caches can maintain coherence by invalidating, updating, or writing back data based on the actions of other caches.

How Snoopy Protocols Work:
- Each processor cache watches the system's shared bus for memory transactions.
- When a cache detects a memory operation (read or write) from another processor that affects data it holds,  it takes appropriate actions to maintain coherence (e.g., invalidating or updating its copy).
- The bus broadcasts information about memory accesses to all caches, and each cache determines whether it needs to act based on the transaction.

For small scale machines.
##### Directory-based Protocols
In directory-based protocols, the system uses a central directory that keeps track of the status of each cache line, specifically which caches hold a copy of a particular memory block. The directory is responsible for managing cache coherence instead of relying on bus snooping.

How Directory-Based Protocols Work:
- A central directory keeps track of the status each block.
- When a processor wants to read or write a memory location, the central directory checks the status of the memory block and notifies the relevant caches.
- The directory can then update relevant caches or invalidate them.





