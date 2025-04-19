#### Static vs. Dynamic Typing

**Static Typing**
- Types are checked at **compile-time**.
- Errors are caught before the program runs.
- Example languages: **C, C++, Java, Rust, Haskell**
- Pros: Better performance, early error detection.
- Cons: Can be verbose (unless type inference helps).

```cpp
int x = 5;  // Statically typed: x is an int
```

**Dynamic Typing**
- Types are checked at **runtime**.
- More flexibility; variables can hold different types.
- Example languages: **Python, JavaScript, Ruby**
- Pros: Concise, good for quick prototyping.
- Cons: Errors show up only at runtime.

```cpp
x = 5      # x is an int
x = "Hi"   # now x is a string — totally fine in dynamic typing
```



#### Strong vs. Weak Typing

**Strong Typing**
- Prevents type coercion unless explicitly allowed.
- More strict about mixing types.
- Example: **Python, Java**

```python
"5" + 5  # TypeError in Python (can't add str and int)
```

**Weak Typing**
- Implicit type conversions are allowed.
- Example: **JavaScript, C**
```cpp

int x = 5;  // Statically typed: x is an int
```


