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

**Advantages**:
- Can recognize almost all programming language constructs expressed in context-free grammars
- Requires no backtracking
- Can detect syntactic error as soon as possible
##### Shift Reduce Parsing
The parser uses:
- A **stack**: stores partially parsed symbols
- **The input buffer**: the remaining input to be parsed
- An **action table**: indexed by terminals and states
	- Tells you to shift or reduce
- A **goto table**: indexed by non terminals and stats
	- Tells you index into a state that tells you which state to goto
	
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

**Motivation**:
When doing shift-reduce by hand, you have to constantly consider:
- Should I shift the next token or reduce something on the stack?
- If I reduce, which rule should I use?

**How to Read the Tables**:
A real parser automates that with a deterministic finite automaton built from grammar items. The automaton is encoded as **two tables:**
- **ACTION** — decides _shift / reduce / accept / error_ on terminals
	- Rows = parser states
	- Columns = terminal symbols
	- Entries
		- `sN` → _shift_ and go to state N
		- `rK` → _reduce_ by production K
		- `acc` → _accept_
		- blank → _error_
- **GOTO** — decides _which state to go to_ on non-terminals after a reduction
	- Rows = same parser states
	- Columns = non-terminals
	- Entries = next state number after reducing a non-terminal

**How they're used**:
At each step, you look at:
1. **Top of the stack → gives current state**
2. **Next input token**
3. **Lookup (state, token) in ACTION table**

Depending on what’s there:
- `sN` → shift that token onto stack, go to state `N`
- `rK` → reduce by production `K` (pop symbols off stack, push its LHS nonterminal, and use the **GOTO** table to find the new state)
- `acc` → accept (input parsed)
- empty → error (invalid syntax)

##### LR(k) Parsing
LR(k) parsing is the **most general form** of deterministic bottom-up parsing.   
It stands for:
- **L** — scan the input **Left-to-right**
- **R** — produce a **Rightmost derivation in reverse**
- **(k)** — use **k lookahead tokens** to make decisions

So, **LR(k)** parsers decide _when to shift or reduce_ based on both:
- the **current parser state**, and
- up to **k upcoming input symbols** (lookahead).

How it works:
Each step:
1. Reads the **current state** (top of stack)
2. Peeks at the **lookahead token**
3. Uses `(state, token)` → **ACTION**
    - `sN` → shift and go to state N
    - `rP` → reduce by production P
    - `acc` → accept
4. When reducing by `A → β`, it:
    - pops |β| symbols and states
    - looks at the new top state `s'`
    - pushes `(A, GOTO[s', A])`

This continues until `$` (end of input) and the start symbol `S` are reduced to acceptance.

What the "k" does:
- In **LR(0)**: parser decides purely from the **state** (no lookahead).  
    → often too weak (many conflicts).
- In **LR(1)**: parser also looks at **1 next token**.  
    → far more powerful and can handle nearly all deterministic CFGs.
- In **SLR (Simple LR)**: uses **FOLLOW sets** to approximate the lookahead.  
    → smaller tables, less powerful.
- In **LALR (LookAhead LR)**: merges compatible LR(1) states to save space.  
    → same power as canonical LR(1) for most programming grammars.

Example:
Consider the following grammar:
![[Pasted image 20251111173828.png]]

Consider the following parsing table:
![[Pasted image 20251111173802.png]]

Consider the following input: `id * id + id`

```
Look at state 0 with input id, the action is s5
Push state 5 onto stack, then consume a symbol of input (id)

Now look at state 5 and *, the action is r6
So reduce on F goes to id. We look at the length of the rhs which is one then pop that many symbols off the stack, 0 is left on stack
Now we look at 0 with left hand side which is F and we index into goto table at (0, F) which tells us to go to state 3, so we push that onto the stack

...
```

![[Pasted image 20251111180134.png]]

##### How To Create the Table?
The states are sets of what are called LR(0) items.

An item is a production with a dot at some point in the right hand side. The dot acts as a cursor, and you're enumerating all the potential states by moving the dot.
```
E → ·E + T     (haven’t seen anything yet)
E → E· + T     (we’ve seen E)
E → E + ·T     (Have seen E+, next expect T)
E → E + T·     (entire RHS seen, ready to reduce)
```

![[Pasted image 20251111182412.png]]

https://www.youtube.com/watch?v=g1G7p9EPDYo

**Closure and Goto Functions**
1. Closure(l)
	Whenever you have an item like `A → α·Bβ` — meaning you’re right before a nonterminal **B** — you need to imagine what **B** could start expanding into.
	- So, for every rule that defines **B**, add a new item for it with the dot at the very beginning.
	- Example: if you have `A → α·Bβ` and `B → x y`, then you also add `B → ·x y`.
2. Goto(l, x)
	Think of **Goto(I, X)** as asking: _“If I’m in these states and I see X next, where can I go?”_
	- You look at every item in **I** where the dot is **right before X** — like `A → α·Xβ`.
	- Then, for each of those, you **move the dot past X**, making it `A → αX·β`.
	- The set of all those new items becomes your starting point.
	- Finally, take the **Closure** of that set to fill in any new possibilities (just like before).

Example:
Consider the following grammar:
```
1. E → E + T  
2. E → T  
3. T → id
```

S1: Augment grammar:
```
0. S' → ·E
```
We’ll call this the starting set **I₀ = { S' → ·E }**.

S2: Compute Closure(I₀):
> Whenever you have a dot before a nonterminal (like `·E`), you must include _all productions of that nonterminal_ with the dot at the beginning.

In `S' → ·E`, the dot is before **E**. So we add **all rules of E**, each with a dot at the start:
```
E → ·E + T  
E → ·T
```

Now our set is:
```
S' → ·E  
E → ·E + T  
E → ·T
```

Now look again — we’ve just added `E → ·T`.
- The dot is before **T**, which is also a nonterminal.
- So we must include all **T** productions, each with a dot at the start.

We add:
```
T → ·id
```

Now our closure is complete — there are no new nonterminals after any dots.

Final Closure(I₀):
```
S' → ·E
E → ·E + T
E → ·T
T → ·id
```

S3: Compute Goto(I₀, X)
**Goto(I, X)** = “What happens if we see `X` next?”

We look at all items in **I₀** where the dot is right before **X**, move the dot past **X**, and then take the **closure** of that new set.

Example -> Goto(I₀, E) 
Look for items with `·E`:
```
S' → ·E
E → ·E + T
```

Move the dot past `E` in both:
```
S' → E·
E → E· + T
```
That’s your starting set.

Now take **Closure**:
- In `S' → E·`, the dot is at the end — nothing to add.
- In `E → E· + T`, the dot is before `+` (a terminal), so nothing to add either.

Goto(I₀, E) = { S' → E·, E → E· + T } = l1

Example -> Goto(I₀, T)
Look for items with `·T`:
```
E → ·T
```

Move the dot past `T`:
```
E → T·
```

Dot is now at the end → no new nonterminals → closure doesn’t add anything.

Goto(I₀, T) = { E → T· } = l2

Example -> Goto(I₀, id)
Look for items with `·id`:
```
T → ·id
```

Move the dot past `id`:
```
T → id·
```

Goto(I₀, id) = { T → id· } = l3

...

Goto(I₀, +) = { E → E + ·T, T → id· } = l4

Goto(I₀, T) = { E → E + T· } = l5

Goto(I₀, id) = { T → id·} = l3 (duplicate)


Now we have:
- **Item sets (states)** → I₀, I₁, I₂, I₃, I₄, I₅
- **GOTO transitions** between them 

```
I₀: S' → ·E, E → ·E + T, E → ·T, T → ·id
I₁: S' → E·, E → E· + T
I₂: E → T·
I₃: T → id·
I₄: E → E + ·T, T → ·id
I₅: E → E + T·
```

Recall the grammar:
```
(0) S' → E
(1) E → E + T
(2) E → T
(3) T → id
```

Identify terminals vs nonterminals
- Terminals: `id`, `+`, `$`
- Nonterminals: `E`, `T`

S4: For each state (I₀–I₅), look at what’s after the dot
That tells you what kind of **table entry** (shift, goto, reduce, or accept) to make.

| What’s after the dot              | Type of move | Table                                           | Meaning                                                         |
| --------------------------------- | ------------ | ----------------------------------------------- | --------------------------------------------------------------- |
| **A terminal (like `id`, `+`)**   | **Shift**    | `ACTION[state, terminal] = shift X`             | “If I see this terminal next, move to state X (advance input).” |
| **A nonterminal (like `E`, `T`)** | **Goto**     | `GOTO[state, nonterminal] = X`                  | “If I just finished parsing this nonterminal, go to state X.”   |
| **Nothing (dot at end)**          | **Reduce**   | `ACTION[state, all terminals] = reduce by rule` | “The RHS is fully seen, so reduce to its LHS.”                  |
| **Dot at end of the start rule**  | **Accept**   | `ACTION[state, $] = accept`                     | “We finished the whole input.”                                  |
```
E → ·E + T      → dot before nonterminal → Goto on E  
E → E· + T      → dot before terminal → Shift on +  
E → E + T·      → dot at end → Reduce by E → E + T  
S' → E·         → start rule done → Accept on $
```

State I₀:
```
S' → ·E
E  → ·E + T
E  → ·T
T  → ·id
```
- Dot before **E** → nonterminal → `Goto(I₀, E) = I₁`
- Dot before **T** → nonterminal → `Goto(I₀, T) = I₂`
- Dot before **id** → terminal → `ACTION[I₀, id] = shift 3`
```
ACTION[I₀, id] = s3
GOTO[I₀, E] = 1
GOTO[I₀, T] = 2
```


State I₁:
```
S' → E·
E  → E· + T
```
- `S' → E·` → dot at end and it’s start → **accept** when `$` comes next.
- `E → E· + T` → dot before `+` → terminal → `ACTION[I₁, +] = shift 4`
```
ACTION[I₁, +] = s4
ACTION[I₁, $] = acc
```

State I₂:
```
E → T·
```
- Dot at end → **reduce by rule (2)**: `E → T`
In LR(0), a reduce applies for _all terminals_, because LR(0) has no lookahead.
```
ACTION[I₂, id] = r2
ACTION[I₂, +]  = r2
ACTION[I₂, $]  = r2
```

**The Big Picture**
1. Start from the **closure** of the augmented start production.
2. Repeatedly take **goto** for every possible symbol (terminal or nonterminal).
3. Each unique closure you get becomes a **state** in your automaton.
4. The `goto` edges between those states form the transition graph

##### Canonical Collection of Sets of LR(0) items
The Canonical Collection of Sets of LR(0) Items is the complete set of parser states that an LR(0) parser can ever be in.

It is called _canonical_ because:
- It’s constructed systematically (not guessed).
- It uniquely represents **all valid configurations** of the parser for a grammar.

**How to construct it**
Step 1: Augment the grammar
Add a new start production:
```
S' → S
```

Step 2. Create the initial item set
Start with:
```
I₀ = closure({ S' → · S })
```

Step 3. Compute transitions
For each item set `I` and each grammar symbol `X` (terminal or nonterminal):
- Compute `goto(I, X)`
- If `goto(I, X)` produces a new, distinct set of items, label it as a new state.

Step 4. Repeat until no new sets appear
When finished, the full collection `{ I₀, I₁, I₂, …, In }` is called the **canonical collection of sets of LR(0) items**.


##### SLR Parsing
**SLR** stands for **Simple LR(1)** (or **SLR(1)**) parsing.

It uses the **same canonical LR(0) items** as an LR(0) parser, but **adds FOLLOW sets** to decide reduce actions more intelligently.

Steps:
1. Augment the grammarc
2. Construct the canonical collection of LR(0) item sets
3. Build the ACTION table (for terminals)
	For each state `Ii`:
	
	If there’s an item `A → α·aβ` where `a` is a **terminal**,  
	then set 
	`ACTION[i, a] = shift j`
	where `goto(Ii, a) = Ij`.

	If there’s an item `A → α·` (dot at the end of a production and `A ≠ S'`),
	then for **every terminal `a` in FOLLOW(A)**, set
	`ACTION[i, a] = reduce A → α`

	If there’s an item `S' → S·`,
	set
	`ACTION[i, $] = accept`

4. Build the GOTO table (for nonterminals)
	For each nonterminal `A`, if `goto(Ii, A) = Ij`, then set
	`GOTO[i, A] = j`

5. Mark all other entries as errors
6. Check for conflicts
	If any cell in the ACTION table has more than one possible action (e.g., both shift and reduce),
	then the grammar is not SLR(1).

![[Screenshot_20251111_211049.png]]

Anita da goat:
- LR(0) items: https://www.youtube.com/watch?v=ZfB4JU2YZ_0
- SLR Parsing Table: https://www.youtube.com/watch?v=8Cq3EIgXOec

Action Table TLDR:
- If a dot is followed by a terminal, then shift to state of goto of that terminal
	- ex: In i0 F->.(E), i2 = goto(I0, ()
	- So in this case you shift to 2
- If the dot is at the end without the previous symbol being the start symbol then 

Goto table TLDR:
- If a dot 