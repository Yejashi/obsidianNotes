SSA (Static Single Assignment) in LLVM is a property of the intermediate representation (IR) where each variable is assigned a value exactly once, and every variable is uniquely defined.

In SSA form:
- Every variable is assigned only once.
- Each use of a variable refers to a single, unambiguous definition.
- No Mutable Variables: Mutable variables are replaced by new definitions for each assignment.

### SSA in Action
Example Before SSA:
```
x = 10;
x = x + 1;
y = x * 2;
```

After SSA:
```
x1 = 10;        ; First assignment to x
x2 = x1 + 1;    ; New definition for x after modification
y1 = x2 * 2;    ; y depends on the latest definition of x
```

### PHI Nodes in SSA
In cases where control flow merges (e.g., after a conditional branch), SSA introduces PHI nodes to select the correct variable version based on the execution path.

Example:
```
if (cond) {
    x = 10;
} else {
    x = 20;
}
y = x + 1;
```

