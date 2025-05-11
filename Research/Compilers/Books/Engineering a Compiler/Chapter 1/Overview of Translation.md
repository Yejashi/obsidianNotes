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

The semantic models that compilers use to reason about programming languages are simpler than the models needed to understand natural language.

A compiler builds mathematical models that detect specific kinds of inconsistency in a program. Compilers check for consistency of type; for example, the expression:
```
a ← a × 2 × b × c × d
```
might be syntactically well-formed, but if b and d are character strings, the sentence might still be invalid.

### Intermediate Representations

The final issue handled in the front end of a compiler is the generation of an ir form of the code.

### The Optimizer

When the front end emits ir for the input program, it handles the statements one at a time, in the order that they are encountered. Thus, the initial ir program contains general implementation strategies that will work in any surrounding context that the compiler might generate

The optimizer analyzes the ir form of the code to discover facts about that context and uses that contextual knowledge to rewrite the code so that it computes the same answer in a more efficient way.

Efficiency can have many meanings. The classic notion of optimization is to reduce the application’s running time. In other contexts, the optimizer might try to reduce the size of the compiled code, or other properties such as the energy that the processor consumes evaluating the code. All of these strategies target efficiency.

##### Analysis
Most optimizations consist of an analysis and a transformation. 

The analysis determines where the compiler can safely and profitably apply the technique.

Compilers use several kinds of analysis to support transformations. Data flow analysis reasons, at compile time,  about the flow of values at runtime. 

**Data-flow analyzers** typically solve a system of simultaneous set equations that are derived from the structure of the code being translated.

**Dependence analysis** uses number-theoretic tests to reason about the values that can be assumed by subscript expressions.
##### Transformation
To improve the code, the compiler must go beyond analyzing it.

The compiler must use the results of analysis to rewrite the code into a more efficient form. 

### The Back End

The compiler’s back end traverses the ir form of the code and emits code
for the target machine.

##### Instruction Selection
