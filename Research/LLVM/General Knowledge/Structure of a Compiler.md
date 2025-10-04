Compiler technology is a well-studied field of computer science. The high-level task is to translate a source language into machine code. Typically, this task is divided into three parts, the **frontend**, the **middle end**, and the **backend**.

### Building Blocks of a Compiler
At a high level, there are three components. The **frontend** turns the source code into an intermediate representation (IR). Then the **middle end** performs transformations on the IR, with the goal of either improving performance or reducing the size of the code. Finally, the **backend** produces machine code from the IR.

### An arithmetic expression language
Arithmetic expressions are a part of every programming language. Here is an example of an arithmetic expression calculation language called **calc**. The calc expressions are compiled into an application that evaluates the following expression:
```
with a, b: a * (4 + b)
```

The used variables in the expression must be declared with the keyword, with. This program is compiled into an application that asks the user for the values of the a and b variables and prints the result.

### Formalism for specifying the syntax of a programming language

