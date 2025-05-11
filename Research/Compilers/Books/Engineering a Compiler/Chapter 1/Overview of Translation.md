To translate code written in a programming language into code suitable for execution on some target machine, a compiler runs through many steps.

### The Front End

Before the compiler can translate an expression into executable target machine code, it must understand both its form, or syntax, and its meaning, or semantics.

#### Checking Syntax
To check the syntax of the input program, the compiler must compare the program’s structure against a definition for the language.

Mathematically, the source language is a set, usually infinite, of strings defined by some finite set of rules, called a *grammar*.

Two separate passes in the front end, called the **scanner and the parser**, determine whether or not the input code is, in fact, a member of the set of valid programs defined by the grammar.