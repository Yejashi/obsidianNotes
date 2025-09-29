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

Note: Use the same derivation scheme both times (e.g leftmost)

![[Pasted image 20250929190737.png]]

