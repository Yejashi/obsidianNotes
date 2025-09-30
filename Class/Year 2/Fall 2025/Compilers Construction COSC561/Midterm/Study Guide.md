### Notes
#### Regular expressions
**epsilon closure:**
- Set of NFA states reachable from NFA state $s$ on e-transitions alone

**Thompson Construction**:
- Way to convert a regular expression to an NFA
	![[Pasted image 20250929194349.png]]

### Converting NFA to DFA
- Create empty transition table
	- The rows correspond to the marked states
	- The columns correspond to the alphabet
- Start by getting epsilon closure of the start state
	- All of the states reachable through epsilon transitions alone
- While there is an unmaked state
	- For each symbol a compute move(T, a)
	- Then calculate its epsilon closure
		- Call that a new state
		- Mark it
- Anything that includes an accepting state will be an accepting state
- *** Remember you can reach yourself with epsilon transition
- When you have an empty state just create a dead state but ignore it when drawing dfa

### Minimizing DFA
- Group your states into groups you know can be distinguished
	- e.g set of states that accept and set of states that dont accept
- Algorithm
	- Lets try different string and see if we can distinguish
	- Keep distinguishing until you cant
- If you have everything as an accepting state, you would just group everything into one state
- If you have a dead state
	- Use the dead state to distinguish
	- For everything in the alphabet, the dead state goes to itself
### Eliminating Left Recursion
**Immediate Left Recursion**:
- Replace A -> Aa| B with  "Memorize"
	- A -> BA'
	- A' -> aA'|e
- Basically identify what should be A, a, and B and do the replacement

**General Algorithm**:
- Create a list of non terminal to enumerate
- Visit each non terminal (i)
	- For the first one, you can eliminate the immediate left recursion
	- For the visited (j)
		- Replace the production of Aj in Ai -> Aj
	- Remove immediate left recursion
	- Remove epsilon
		- Anywhere A' appears add a production where you took no input
![[Pasted image 20250930033225.png]]

### Predictive Parsers
**LL Parser**
- An **LL parser** is a type of top-down parser for context-free grammars
- **L** = Left-to-right scan of the input
- **L** = Leftmost derivation of the parse tree
So, an LL parser reads input from **left to right** and builds a **leftmost derivation**
It predicts which production rule to apply using a lookahead of some number of input symbols.
![[Pasted image 20250930044057.png]]

![[Pasted image 20250930044038.png]]

**How is a predictive parsing table created?**
- FIRST(a):  set of terminals that begins strings derived from a. if a is epsilon or generates epsilon, then epsilon is also in FIRST(a)
	![[Pasted image 20250930052505.png]]
	 TLDR: set of terminals that can appear **first** in some string derived from α
- FOLLOW(a): Set of terminals that can immediately follow A in a sentenial form. 
	- ![[Pasted image 20250930052803.png]] 
	  TLDR: set of terminals that can appear immediately to the right of A in some sentential form 
	  Steps:
		- For FOLLOW(X) look where X is in the right hand side then follow the rules.
	 ![[Pasted image 20250930053022.png]] 
- ![[Pasted image 20250930071035.png]]
### Study Guide ![[Pasted image 20250929190113.png]]

A grammar is considered ambiguous if you can derive the same string from it.

For example:
```
String = ()

Derivation 1:
S --> (S) --> ()

Derivation 2:
S --> SS --> (S)S --> ()S --> ()
```

**Note: Use the same derivation scheme both times (e.g leftmost)**

![[Pasted image 20250929190737.png]]
![[Pasted image 20250930012825.png]]
```lua
*
└─ concat
   ├─ * 
   │  └─ |
   │     ├─ concat
   │     │  ├─ 'a'
   │     │  └─ 'b'
   │     └─ ε
   └─ 'c'
```

![[Pasted image 20250930013026.png]]

![[Pasted image 20250930020756.png]]
![[Pasted image 20250930020810.png]]


![[Pasted image 20250930021003.png]]
![[Pasted image 20250930031026.png]]
![[Pasted image 20250930031105.png]]

![[Pasted image 20250930031301.png]]
![[Pasted image 20250930035600.png]]

![[Pasted image 20250930042351.png]]

![[Pasted image 20250930042440.png]]
![[Pasted image 20250930051031.png]]



![[Pasted image 20250930044119.png]]

![[Pasted image 20250930044137.png]]

![[Pasted image 20250930044153.png]]


#### Short Answers
1. What is a compiler?
	- A compiler is a translator program that reads a program written in a source language and translates it to an equivalent program written in a target language.

2. Explain the difference between a compiler and an interpreter. Give one example of interpreted language and compiled language
	1. 

3. Name and provide a one-line description of the six compiler phases
	- **Lexical Analyzer (Scanner):** Breaks the source code into tokens (keywords, identifiers, operators, etc.).
	- **Syntax Analyzer (Parser):** Checks the token stream against grammar rules to build a parse tree.
	- **Semantic Analyzer:** Ensures correctness of meaning (type checking, scope resolution, etc.).
	- **Intermediate Code Generator:** Translates the parse tree into an intermediate representation (IR) closer to machine code but still abstract.
	- **Code Optimizer:** Improves the intermediate code for efficiency (speed, memory usage, etc.) without changing its behavior.
	- **Code Generator:** Converts optimized IR into target machine code and generates the final executable.
