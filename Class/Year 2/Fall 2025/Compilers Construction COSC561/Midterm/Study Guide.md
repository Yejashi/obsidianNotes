### Notes
#### Regular expressions
**epsilon closure:**
- Set of NFA states reachable from NFA state $s$ on e-transitions alone

**Thompson Construction**:
- Way to convert a regular expression to an NFA
	![[Pasted image 20250929194349.png]]


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

