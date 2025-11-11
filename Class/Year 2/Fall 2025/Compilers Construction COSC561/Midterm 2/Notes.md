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

Look at where it gets applie don the right hand side and apply rules.
Rules of thumb:
1. Start symbol rule:
	add `$` to FOLLOW(S) 
2. When A → α B β:
	add (FIRST(β) - ε) to follow B.
3. When A → α B or A → α B β where β ⇒ ε:**
	Add FOLLOW(A) to FOLLOW(B)
	(Because once β disappears, what comes after A now comes after B.)

```
E → T E'
E' → + T E' | ε
T → F T'
T' → * F T' | ε
F → (E) | id
```

Start: FOLLOW(E) = { $, ) }
(Since E can appear inside parentheses or at the top.)
In E → T E':
FOLLOW(T) ⊇ FIRST(E') − {ε} = { '+' }
Since E' ⇒ ε, FOLLOW(T) also gets FOLLOW(E) = { ), $ }
In T → F T':
FOLLOW(F) ⊇ FIRST(T') − {ε} = { '*' }
Since T' ⇒ ε, FOLLOW(F) ⊇ FOLLOW(T) = { '+', ), $ }

#### Bottom-Up Parsing
Goal: Construct a parse tree for an input string beginning at the leaves and working towards the root.
- Essentially the process of reducing the string to the start symbol.
- Bottom-up parsing constructs the right-most derivation in reverse.

At each step in the parse, two decisions need to be made
- When to reduce
- What production to apply

Bottom-up parsers can be written for the set of grammars known as **LR** grammars.
- L because we're still scanning the input form left to right
- R because we're producing a right most derivation

All LL grammars can be parsed with a bottom-up parser. All LR grammars can be parsed using a bottom-up parser, but some cannot be parsed with a top-down (LL) parser.

The parser uses:
- A **stack**: stores partially parsed symbols
- **The input buffer**: the remaining input to be parsed
- An **action table**: indexed by terminals and states
	- Tells you to shift or reduce
- A **goto table**: indexed by non terminals and stats
	- Tells you index into a state that tells you which state to goto
##### Core Mechanism: "Shift"  and "Reduce"

Vocab:
- A **handle** is a substring that matches the rhs of a production

At each step you do one of four possible actions:
- **Shift**: Move the next input symbol onto the stack
- **Reduce**: replace rhs of production that is found on the stack with the nonterminal on the left of that production
- **Accept**: If the stack has only the start symbol and the input is `$`, the parser accepts
- **Error**: No valid action, input doesnt match grammar

The Key Intuition: Finding the “Handle”
- Each reduction replaces a handle — a substring that corresponds to a right-hand side (RHS) of some production and could appear next in a rightmost derivation.

In plain words:
	A _handle_ is a piece of the input that “fits perfectly” to collapse back into a nonterminal.

Example:
Consider the grammar:
```
E → E + T | T
T → T * F | F
F → (E) | id
```

In `id + id * id`, after reading `id`, the substring `id` is a handle for `F → id`.  
Later, `id * id` becomes a handle for `T → T * F`, etc.

Bottom-up parsing’s job is to discover handles and reduce them in the correct order.

Quick by hand example, on input `id + id * id $`, one plausible sequence is:
```
Stack        | Input           | Action
-------------+-----------------+---------
$            | id + id * id $  | shift id
$ id         | + id * id $     | reduce F→id
$ F          | + id * id $     | reduce T→F
$ T          | + id * id $     | reduce E→T
$ E          | + id * id $     | shift '+'
$ E +        | id * id $       | shift id
$ E + id     | * id $          | reduce F→id
$ E + F      | * id $          | reduce T→F
$ E + T      | * id $          | shift '*'
$ E + T *    | id $            | shift id
$ E + T * id | $               | reduce F→id
$ E + T * F  | $               | reduce T→T*F
$ E + T      | $               | reduce E→E+T
$ E          | $               | accept
```

##### How does the parser know when to shift or reduce?
That's where **ACTION** and **GOTO** tables come in.

**Motivation**
When doing shift-reduce by hand, you have to constantly consider:
- Should I shift the next token or reduce something on the stack?
- If I reduce, which rule should I use?

A real parser automates that with a deterministic finite automaton built from grammar items. The automaton is encoded as **two tables:**
- **ACTION** — decides _shift / reduce / accept / error_ on terminals
- **GOTO** — decides _which state to go to_ on non-terminals after a reduction


