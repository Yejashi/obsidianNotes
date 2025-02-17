## Lecture 5

How do measure ?
- Worst cast
- Average case
- Stability
- Other? For example, out of core.

Average case analysis of quicksort
- Assume keys are distinct
- Assume all permutations are equally likely

Let F(n) denote the average number of comparisons required

Then F(n) = (n-1) + (1/n) * $\sum$ (i = 1, n) [F(i-1) + F(n-i])]
 
 which by symmetry = (n-1) + (2/n)$\sum$ (i=1,n)[F(i-1)]
 - this is a first order homogenous recurrence
 - It requires a change of variable
 - Then uses asymptotics (~) to convert a series to an itegral.
 - And finally find that F(n) is about 1.39 nlog2n   

Back to quicksort
- Its average case is excellent.
	- But the analysis assumes that keys are distinct, and that all permutation are equally likely.
	- MOreover, the worst case is truly awful.
		- Can we address this?
		- And if so, is the cure worse than the disease.
Algorithm 1
- Identify the smallest, then the next smallest, etc
- COntinue until we find the nearest $n/2$ smallest.

Algorithm 2
- Sort the file
- Use the item at location $n/2$ .

Algorithm 3:
- Pseudo-randomly pick a small set of elements
- Use their median as a proxy

Algorithm 4.
- Break the file into subfiles
- Find the median of each suffle
- Compute the median of medians

The median of medians approach
- CHoose an r > 1 (for file size)
- As we'll see, it turn out that 5 is a good choice
- Divide L into n/r subfiles
- Find the median of each subfile
- Find the median of medians

![[IMG_1213.jpg]]

Obserbe:
- Every element o A is at most m
- Every elemend of D is at least m
- Partition with m, and L  is split into two subfiles each with n/4 or more elements
Hence the recurrence:
- t(n) = c1n for small n
- t(n) = c2n + t(n/5) + t(3n/4) otherwise
-          [find mednian] + [find m]  +  [find the kth largest element]
it turns out that t(n) is o(n)

So we can make quicksort o(nlogn) even in the worst case. And a more careful look at our figure reveals that the last termis actually a wee but smaller at T(7n/10)


## Lecture 6

Decision tree for evaluating algorithms

stirlings approximation

record moves, key comparisons

radix sort

chapter 10, elementary datastructures
- 


## Lecture 7

#### DYNAMIC PROGRAMMING

Dynamic programming (DP) is an algorithmic paradigm used to solve complex problems by breaking them into simpler, overlapping subproblems. It is especially powerful for multi-stage decision processes, where the final solution is built step by step from solutions to smaller subproblems.

#### 1. DP Amenability: Multi-Stage Decision Process
Many optimization problems can be naturally divided into stages. In a typical multi-stage decision process:

- **Stages:** The problem is divided into N stages.
- **Decision Options:** At each stage, you have d possible decisions.
- **Brute-Force Complexity:** Without DP, you might explore $O(d^N)$ possible decision sequences.
- **Dynamic Programming Advantage:** DP avoids redundant work by storing intermediate results and building the overall solution efficiently.

#### 2. Classic Examples of DP
Dynamic programming has been successfully applied in various fields. Some classic examples include:
- **Job Sequencing:** Scheduling tasks in an order that optimizes overall performance or cost.
- **Tape Utilization:** Optimally storing data on tape where order and grouping affect retrieval efficiency.

#### 3. The Knapsack Problem as a DP Example
One of the hallmark examples in DP is the **Knapsack Problem**:
- **Problem Statement:**  
    Given a set of items—each with an associated value and size—and a knapsack with a fixed capacity, select a subset of items that maximizes the total value without exceeding the capacity.
    
- **Fractional vs. 0/1 Knapsack:**
    - In the _fractional knapsack problem_, items can be divided; a simple greedy algorithm (choosing items based on value-to-weight ratio) finds the optimum.
    - In the _0/1 knapsack problem_, items are indivisible (each item is either taken or left).
        - A naive approach would consider every item’s inclusion (yes/no), leading to $O(2^n)$ possibilities.
        - Here, each item can be viewed as a stage with two decisions (include or exclude), making it a natural multi-stage decision process.

#### 4. Key Challenges in Formulating a DP Solution
When setting up a DP formulation, several practical issues must be addressed:
- **Formulation:** How to define the state, decision, and return variables that capture the essence of the problem.
- **Tracking Partial Solutions:** Efficiently keeping track of solutions to subproblems (often via a DP table).
- **Ensuring Completeness:** Making sure that all possible decision sequences are considered without unnecessary repetition.
- **Avoiding Loops:** Preventing infinite loops or redundant recalculations.
- **Efficiency:** Balancing the trade-off between time and space—DP often uses extra memory (to store subproblem solutions) to save computational time.

**Solution Strategy:**
- Use a DP table (or memoization) for each stage.
- Prune or avoid considering suboptimal partial solutions.
- Store (cache) intermediate results so that each subproblem is solved only once—this is the essence of “trading space for time.”

#### 5. Notation and Variables in DP
At each stage i of a DP formulation, we typically define:
- **$s_i$(State Variable):** Represents the condition or configuration of the system at stage i.
- $d_i$ **(Decision Variable):** The choice made at stage i.
- **$r_i$​ (Return Variable):** The cumulative “reward” or cost from stage i onward.

An asterisk (e.g., $r_i^*$, $d_i^*$) denotes the **optimal** value or decision for that stage.


#### 6. The Backwards Approach and Process Diagram
Dynamic programming often uses a _backwards_ (or “backward induction”) approach:
- **Concept:** Start at the final stage where the outcome is known, and work backwards to determine the optimal decision at each preceding stage.

**Process Diagram (Conceptual):**  
Imagine a flowchart where:
- The final stage provides a known return.
- At each stage i, you compute the optimal return $r_i^*(s_i)$ as: $r_i^*(s_i) = \max_{d_i \in D(s_i)} \left\{ r_i(s_i, d_i) + r_{i+1}^*(s_{i+1}) \right\}$
- The decision  $d_i^*$ that maximizes this expression is the optimal decision at stage i.

![[Pasted image 20250211164659.png]]

#### 7. Bellman's Principle of Optimality
Dynamic programming is built on **Bellman's Principle of Optimality**, which states:

> _An optimal decision sequence has the property that, regardless of the initial state and decision, the remaining decisions must form an optimal sequence for the resulting state._

In other words, if you have an optimal path (or decision sequence) from stage 1 to N, then for any intermediate stage i, the remaining sequence from i to N must also be optimal given the state at stage i.

This principle underpins the recursive structure of the DP formulation.


#### DP Table Format and Example Structure

When implementing a DP solution (for example, for the 0/1 knapsack problem), the DP table is structured as follows:
- **Rows:** Often represent the state (or remaining capacity in knapsack problems).
- **Columns:** Represent the decisions (or items being considered).
- **Entries:** Each cell in the table stores the optimal value (or cost) achievable with a given state and set of decisions.

![[Pasted image 20250211165305.png]]

For the 0/1 knapsack problem:
- The table has one dimension for the items (each item being a stage) and another for the remaining capacity.
- The table is filled using a recurrence relation that compares the value of including an item versus excluding it.

For the 0/1 knapsack problem example, the DP table is organized with five key columns:
- **Row Header:** Identifies the current stage or state.
- **Decision Parameter Headers:** Label the different decision scenarios.
- **0 Decision Column:** Shows the result if you decide _not_ to include the item.
- **1 Decision Column:** Shows the result if you decide to include the item.
- **Best Decision Column:** Indicates the optimal decision (either 0 or 1) for that stage.

**For homework, a table for each stage.**

## Lecture 8

A Good Example – Reliability Design – Well Known within the Operations Research Community.
- The goal is to determine the optimal replication (number of copies) of various device types—arranged in series—with each device having multiple copies in parallel to enhance reliability, all while adhering to a total cost constraint.

#### 1. Problem Formulation
We are given:
- **Device Types:** n different types, each connected in series.
- **Replication:** For each device type i, you can choose $m_i$​ copies arranged in parallel.
- **Costs:** Each copy of device type i has cost $c_i​$.
- **Reliability:** The reliability of a single device of type i is $\Phi_i(1)$.
- **System Reliability:** Since devices are in series, the overall system reliability is the product of the reliabilities at each stage: $\text{System Reliability} = \prod_{i=1}^n \Phi_i(m_i)$
- **Cost Constraint:** The total cost must not exceed C :  $\sum_{i=1}^n c_i m_i \leq C$
- **Decision Variables:** Each $m_i$​ must be a positive integer.

For example, suppose:
- n=10 (types)
- C=10 (total cost)
- $c_i$=1 (cost per device) 
- while $\Phi_i$(1)=0.9 (reliability of a single device) for all i.

Then $m_i$ is 1 for all i, and $\prod_{i=1}^n \Phi_i(m_i)$ = 0.35 (system reliability)

#### 2. Modeling Device Replication
If a single device of type i has reliability $\Phi_i(1)$, then the probability of failure is $1 - \Phi_i(1)$.

Assuming independent failures, the probability that all $m_i$ copies fail is $(1 - \Phi_i(1))^{m_i}$.

Thus, the reliability when using $m_i$​ copies is: $\Phi_i(m_i) = 1 - \left(1 - \Phi_i(1)\right)^{m_i}$

_Example:_ If Φi(1)=0.9, then for $m_i=2$: $\Phi_i(2) = 1 - (0.1)^2 = 0.99$

## Lecture 8

![[Pasted image 20250213160806.png]]

So how do we build the dp tables?

Rows? We know the state variable range. it's [0, 105]

Columns? We need to know what values a decision variable can take. Use mi <= i loor(C - Sum(1 <= j <= n)ci + ci) / ci). we need to find m1 in [1,2], m2 in [1,3] and m3 in [1,3]

![[Pasted image 20250213161519.png]]

![[Pasted image 20250213161926.png]]

![[Pasted image 20250213162803.png]]

So 
- the reliability is maximized at .648
- realized with the solution m1 = 1 and m2 = m3 = 2
- and at a cost of 100 < c = 105