# Question 1
Use Figure 4.37 and the expression grammar 4.1 to parse the string (id * id) + id using the LR parsing algorithm.

![[Screenshot_20251112_074220.png]]

![[Screenshot_20251112_074723.png]]

![[Pasted image 20251112081241.png]]

# Question 2
Given the following grammar construct the LR(0) sets of items.
![[Screenshot_20251112_081447 1.png]]
![[Pasted image 20251112100317.png]]
# Question 3
![[Pasted image 20251112105123.png]]

# Question 4
Given the following grammar construct the LR(1) sets of items.
![[Pasted image 20251112105949.png]]
![[Pasted image 20251112152046.png]]

# Question 5
Use the grammar and the set of items in the last problem to construct the canonical parsing table
![[Pasted image 20251112155432.png]]


# Question 6
Draw the DAG representation for the following expression (as shown in Figure 6.3). Provide the quadruple, triple and indirect triple representations of the expression.
```
(a ∗ c) + b ∗ (a ∗ c) + b − (a ∗ c)
```

# Question 10
(a) Why is bottom-up parsing (with one symbol of lookahead) more powerful than top-down parsing (with one lookahead symbol)?

Bottom-up (LR) parsers can handle a **larger class of context-free grammars** than top-down (LL) parsers.
-  LL(1) parsers require grammars to be **left-factored and free of left recursion**, which limits their expressiveness.
- LR(1) parsers work **without modifying the grammar**, handling **left recursion and ambiguity resolution** automatically using a deterministic PDA. As such,  LR(1) parsing can recognize more grammars than LL(1)

(b) Explain the different error recovery strategies.
**Panic-mode recovery** – Keep parsing until a synchronizing token is found. (e.g. semicolon)
**Phrase-level recovery** – Replace the prefix of the remaining input with some string that will
allow the parser to continue looking for errors.
**Error productions** – Augment the grammar for the source language to include
productions for common errors