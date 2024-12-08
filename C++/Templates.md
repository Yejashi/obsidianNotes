Templates are a powerful feature that allows you to write generic and reusable code. 

Templates enable you to define functions, classes, and structures that work with any data type, without specifying the type explicitly at the time of writing the code.

There are two main types of templates in C++:

### Function Templates
Function templates allow you to write a function that can operate on different types of data. The type to be used in the function is determined when the function is called.

Example of a function template:
```cpp
template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    int resultInt = add(3, 4);      // Calls add<int>(3, 4)
    double resultDouble = add(3.5, 4.5);  // Calls add<double>(3.5, 4.5)
    return 0;
}
```


