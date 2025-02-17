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


Issues
- how to set up DP forumulation?
- hot to keep track of partial solutions?
- hot to ensure that all possibilities are considered?
- hot to keep from looping?
- hot to do all this efficiently?

Answer
- keep a dp table for each stage
- avoid considerable of non optimal sub solutions
- avoid re computation of optimal sub solutions
- trade space for time

Variables
- at stage i
	- si = state variable
	- di = decision variable
	- ri = return variable
- where a * superscript denotes optimization

A process diagram
![[Pasted image 20250211164659.png]]
- this is the so called backwards approach
- The optimum return ri*(si) = in or max{ri + ri-1 * (si-1)}), wherethe optimum decision is di*


richard bellman

THe principle of optimzlity
An optimum decision sequence must have the property that for stage i no matter how erver chosen si and di the subsequent decisions di+1, di+2,...dn will be best possible for si and di

DP Table Format
![[Pasted image 20250211165305.png]]

COlumn headers -> decisions you make
For the o1 knapsact problem there are 5 column headers
	Row header, column headers, o decision, 1 descision, best decision
For homerwork, a table for each stage


A goog example - reliable design - well known within the Operations Research COmmunity

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