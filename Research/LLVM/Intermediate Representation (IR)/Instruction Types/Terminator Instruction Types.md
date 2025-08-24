`ret` (**ReturnInst**)
- **Purpose**: End a function by returning control (and possibly a value) to the caller.
- **Details**:
	- Either returns a value of the function’s return type, or `void`.
	- Every non-`void` function must end with a `ret` returning a value.
- **Example**:
```
define i32 @foo(i32 %x) {
entry:
  %add = add i32 %x, 1
  ret i32 %add
}
```

`br` (BranchInst)
- **Purpose**: Explicit jump to another basic block.
- **Details**:
	- Can be **unconditional** (one successor) or **conditional** (two successors).
	- Conditional requires an `i1` condition value.
- **Example**:
```
; unconditional
br label %target

; conditional
%cond = icmp eq i32 %x, 0
br i1 %cond, label %iftrue, label %iffalse

```


`switch` (SwitchInst)
- **Purpose**: Multi-way branch based on an integer value (generalization of `br`).
- **Details**:
	- Compares a value against multiple constant cases.
	- Every non-`void` function must end with a `ret` returning a value.
- **Example**:
```
define i32 @foo(i32 %x) {
entry:
  %add = add i32 %x, 1
  ret i32 %add
}
```


`ret` (**ReturnInst**)
- **Purpose**: End a function by returning control (and possibly a value) to the caller.
- **Details**:
	- Either returns a value of the function’s return type, or `void`.
	- Every non-`void` function must end with a `ret` returning a value.
- **Example**:
```
define i32 @foo(i32 %x) {
entry:
  %add = add i32 %x, 1
  ret i32 %add
}
```


`ret` (**ReturnInst**)
- **Purpose**: End a function by returning control (and possibly a value) to the caller.
- **Details**:
	- Either returns a value of the function’s return type, or `void`.
	- Every non-`void` function must end with a `ret` returning a value.
- **Example**:
```
define i32 @foo(i32 %x) {
entry:
  %add = add i32 %x, 1
  ret i32 %add
}
```


`ret` (**ReturnInst**)
- **Purpose**: End a function by returning control (and possibly a value) to the caller.
- **Details**:
	- Either returns a value of the function’s return type, or `void`.
	- Every non-`void` function must end with a `ret` returning a value.
- **Example**:
```
define i32 @foo(i32 %x) {
entry:
  %add = add i32 %x, 1
  ret i32 %add
}
```



`ret` (**ReturnInst**)
- **Purpose**: End a function by returning control (and possibly a value) to the caller.
- **Details**:
	- Either returns a value of the function’s return type, or `void`.
	- Every non-`void` function must end with a `ret` returning a value.
- **Example**:
```
define i32 @foo(i32 %x) {
entry:
  %add = add i32 %x, 1
  ret i32 %add
}
```


