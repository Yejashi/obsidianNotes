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

The elements of a language, for example, keywords, identifiers, strings, numbers, and operators, are called **tokens**. In this sense, a program is a sequence of tokens, and the grammar specifies which sequences are valid.

Usually, grammar is written in the **extended Backus-Naur form (EBNF)**. A rule in grammar has a left and a right side. The left side is just a single symbol called **non-terminal**. The right side of a rule consists of **non-terminals**, tokens, and meta-symbols for alternatives and repetitions.

**BNF (Backus–Naur Form)** is a formal notation used to describe the syntax of programming languages.
A simple example in BNF:
```
<expr> ::= <term> | <term> "+" <expr>
<term> ::= <factor> | <factor> "*" <term>
<factor> ::= "(" <expr> ")" | <number>
<number> ::= "0" | "1" | ... | "9"
```
BNF uses:
- `::=` for definition (“is defined as”)
- `< >` for nonterminals
- literal characters (like `"+"`, `"("`, etc.) for terminals

**extended Backus-Naur form**
- It adds **extra operators and notation** to make grammars more compact and readable, without changing what they represent.
- Example comparison
	- BNF: `<expr> ::= <term> | <term> "+" <expr> | <term> "-" <expr>`
	- EBNF: `expr = term { ("+" | "-") term } ;`
	
**Common EBNF Extensions**

| Symbol                    | Meaning                      | Example           | Equivalent BNF      |
| ------------------------- | ---------------------------- | ----------------- | ------------------- |
| `[...]`                   | Optional (0 or 1 times)      | `["-"] digit+`    | `<opt_sign> ::= "-" |
| `{...}`                   | Repetition (0 or more times) | `{digit}`         | `<digits> ::= ε     |
| `(...)`                   | Grouping                     | `(A               | B) C`               |
| `                         | `                            | Alternatives (OR) | `A                  |
| `+` (in ANTLR-style EBNF) | One or more                  | `digit+`          | `digit digit*`      |
| `?` (in ANTLR-style EBNF) | Optional group               | `(sign)?`         | same as `["sign"]`  |
| `*` (in ANTLR-style EBNF) | Zero or more                 | `(expr)*`         | same as `{expr}`    |

Now, let’s have a look at the grammar of the calc language:
```
calc : ("with" ident ("," ident)* ":")? expr ;
expr : term (( "+" | "-" ) term)* ;
term : factor (( "*" | "/") factor)* ;
factor : ident | number | "(" expr ")" ;
ident : ([a-zAZ])+ ;
number : ([0-9])+ ;
```

That’s an EBNF grammar with:
- `?` → optional (`("with" ...)` may appear once or not at all)
- `*` → repetition (e.g., `( "," ident)*`)
- `+` → one or more occurrences (e.g., `[a-zA-Z]+`)
- parentheses for grouping

### Lexical Analysis
The task of the lexical analyzer is to take the textual input and create a sequence of tokens from it.

The **calc** language consists of the tokens with, :, +, -, *, /, (, ), and regular expressions ([a-zA-Z])+ (an identifier) and ([0-9])+ (a number). 

We assign a unique number to each token to make the handling of tokens easier.

#### A Hand-Written Lexer
The implementation of a lexical analyzer is often called Lexer. Let’s create a header file called `Lexer.h` and get started with the definition of `Token`. 

It begins with the usual header guard and the inclusion of the required headers:
```
#ifndef LEXER_H
#define LEXER_H
#include "llvm/ADT/StringRef.h"
#include "llvm/Support/MemoryBuffer.h"
```




