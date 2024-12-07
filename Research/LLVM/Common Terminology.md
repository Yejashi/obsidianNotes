Labels are used to refer to the result value of an instruction in an LLVM IR.
```ll
%sum = add i32 %a, 10
```
`%sum` is a definition.

```
%cond = icmp eq i32 %sum, 99
```

`%cond` is a user of `%sum`.

