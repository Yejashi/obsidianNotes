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


