### Things to Know
- Syntax Analysis
	- Bottom-Up Parsing
		- LR parsing algorithm
		- Construct LR(0) sets of items for grammar
		- Construct SLR parsing table
		- Construct LR(1) sets of items for grammar
		- Construct canonical parsing table
	- Error Handling
		- Different error recovery strategies
- Intermediate Code generation
	- Draw DAG
	- Three address code
	- Translate statement with backpatching
	- Translate statement without backpatching
	- Translating switch statements
- Code Generation
- Garbage Collection
### Syntax Analysis

#### Calculating FIRST and FOLLOW
What do they both mean?
- FIRST(X) = "What could appear first if i start expanding X?"
- FOLLOW(X) = "What could appear right after X in a valid sentence?"

##### Intuition for FIRST
Suppose nonterminal `A` is being expanded.

To know which rule to use, ask:
	"What's the first terminal i might see when A starts producing symbols?"

Rules of Thumb
1. if X is a terminal:
	-> FIRST(X) = {X}
	(it literally starts with itself)
2. if X -> epsilon 
	-> FIRST(X) = {epsilon}
3. If X -> Y1, Y2...Yk"
	-> Start from the left:
		Add FIRST(Y1) to FIRST(X)
		If Y1 can be epsilon, add FIRST(Y2), and so on
		If all Y's can be epsilon, add epsilon to FIRST(X)

```
E → T E'
E' → + T E' | ε
T → F T'
F → (E) | id
```

Let's compute FIRST for the above grammar:
- FIRST(E) = FIRST(T) = FIRST(F) = {(, id}
- FIRST(E') = {+, epsilon}
- FIRST(T) = FIRST(F) = {(, id}
- FIRST(F) = {(, id}

##### Intuition for FOLLOW
FOLLOW tells you what can appear immediately after a nonterminal in some valid sentence

To know which rule to use, ask:
	"If I see A in the middle of a derivation, what terminals could come right after it?”

Rules of thumb:
1. Start symbol rule:
	add `$` to FOLLOW(S) 
2. When A → α B β:
	add (FIRST(β) without ε) can follow B.
3. When A → α B or A → α B β where β ⇒ ε:**
	Whatever can follow A can also follow B.
	(Because once β disappears, what comes after A now comes after B.)

```
E → T E'
E' → + T E' | ε
T → F T'
T' → * F T' | ε
F → (E) | id
```

