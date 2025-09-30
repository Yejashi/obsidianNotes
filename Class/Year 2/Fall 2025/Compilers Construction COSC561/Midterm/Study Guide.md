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
- When you have an empty state just create a dead state 
### Study Guide
![[Pasted image 20250929190113.png]]

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
