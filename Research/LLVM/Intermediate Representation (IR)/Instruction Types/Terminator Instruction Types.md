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
	- Always has a _default_ destination if no case matches.
- **Example**:
```
switch i32 %val, label %default [
  i32 0, label %case0
  i32 1, label %case1
]
```


`indirectbr` (IndirectBrInst)
- **Purpose**: Jump to a block whose address is computed at runtime.
- **Details**:
	- Takes a pointer to a basic block label (`blockaddress`).
	- Must list all possible destination blocks statically.
- **Example**:
```
indirectbr i8* %addr, [label %bb1, label %bb2, label %bb3]
```


`invoke` (InvokeInst)
- **Purpose**: Function call with _exception handling support_.
- **Details**:
	- Similar to `call`, but has **two successors**:
		- _normal destination_ (if call returns normally),
		- exception destination (if it throws).
	- Used in EH personality functions + landing pads.
- **Example**:
```
invoke void @may_throw()
        to label %ok unwind label %lpad
```


`resume` (ResumeInst)
- **Purpose**: Resume propagating an exception caught by a `landingpad`.
- **Details**:
	- Takes the exception object from the `landingpad` and continues unwinding.
	- Used in the “old” landingpad-based EH model.
- **Example**:
```
%lp = landingpad { i8*, i32 }
        cleanup
resume { i8*, i32 } %lp
```



`unreachable` (UnreachableInst)
- **Purpose**: Marks code paths that can **never be executed**.
- **Details**:
	- Tells the optimizer that control flow should never reach here.
	- Often used after `llvm.trap`, failed `assume`, or impossible switches.
	- No successors.
- **Example**:
```
call void @llvm.trap()
unreachable
```


