To translate code written in a programming language into code suitable for execution on some target machine, a compiler runs through many steps.

### The Front End

Before the compiler can translate an expression into executable target machine code, it must understand both its form, or syntax, and its meaning, or semantics.

#### Checking Syntax
To check the syntax of the input program, the compiler must compare the program’s structure against a definition for the language.

Mathematically, the source language is a set, usually infinite, of strings defined by some finite set of rules, called a *grammar*.

Two separate passes in the front end, called the ***scanner and the parser***, determine whether or not the input code is, in fact, a member of the set of valid programs defined by the grammar.

**Scanner**: the compiler pass that converts a string of characters into a stream of words

Consider a sentence like “Compilers are engineered objects.” 

The scanner takes a stream of characters and converts it to a stream of classified words -- that is, pairs of the form (p,s), where p is the word’s part of speech and s is its spelling.

A scanner would convert the example sentence into the following stream of classified words:
```
(noun,“Compilers”), (verb,“are”), (adjective,“engineered”), (noun,“objects”), (endmark,“.”)
```

In the next step, the compiler tries to match the stream of categorized words against the rules that specify syntax for the input language.

![[Pasted image 20250510213919.png]]

The derivation proves that the sentence “Compilers are engineered objects.” belongs to the language described by Rules 1 through 6. The sentence is grammatically correct. The process of automatically finding derivations is called **parsing**.

A grammatically correct sentence can be meaningless. For example, the sentence “Rocks are green vegetables” has the same parts of speech in the same order as “Compilers are engineered objects,” but has no rational meaning. To understand the difference between these two sentences requires contextual knowledge about software systems, rocks, and vegetables.


