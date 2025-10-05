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

The `llvm::MemoryBuffer` class provides read-only access to a block of memory, filled with the content of a file. On request, a trailing zero character ('\x00') is added to the end of the buffer. We use this feature to read through the buffer without checking the length of the buffer at each access

 The `llvm::StringRef` class encapsulates a pointer to a C string and its length. Because the length is stored, the string need not be terminated with a zero character ('\x00') like normal C strings. This allows an instance of StringRef to point to the memory managed by `MemoryBuffer`.

With this in mind, we begin by implementing the Lexer class:
1. First, the Token class contains the definition of the enumeration for the unique token numbers mentioned previously:
```
class Lexer;

class Token {
	friend class Lexer;
public:
	enum TokenKind : unsigned short {
		eoi, unknown, ident, number, comma, colon, plus,
		minus, star, slash, l_paren, r_paren, KW_with
	};
```
Besides defining a member for each token, we added two additional values: `eoi` and `unknown`. `eoi` stands for end of input and is returned when all characters of the input are processed. `unknown` is used in the event of an error at the lexical level, e.g., # is no token of the language and would therefore be mapped to unknown.


2. In addition to the enumeration, the class has a `Text` member, which points to the start of the text of the token. It uses the `StringRef` class mentioned previously:
```
private:
	TokenKind Kind;
	llvm::StringRef Text
	
public:
	TokenKind getKind() const { return Kind; }
	llvm::StringRef getText() const { return Text; }
```
This is useful for semantic processing, e.g., for an identifier, it is useful to know the name.

3. The `is()` and `isOneOf() `methods are used to test whether the token is of a certain kind. The `isOneOf() `method uses a variadic template, allowing a variable number of arguments:
```
bool is(TokenKind K) const { return Kind == K; }
bool isOneOf(TokenKind K1, TokenKind K2) const {
	return is(K1) || is(K2);
}
template <typename... Ts>
bool isOneOf(TokenKind K1, TokenKind K2, Ts... Ks) const {
	return is(K1) || isOneOf(K2, Ks...);
}
};
```

4. The `Lexer` class itself has a similar simple interface and comes next in the header file:
```
class Lexer {
	const char *BufferStart;
	const char *BufferPtr;
public:
	Lexer(const llvm::StringRef &Buffer) {
		BufferStart = Buffer.begin();
		BufferPtr = BufferStart;
	}
	void next(Token &token);
private:
	void formToken(Token &Result, const char *TokEnd,
		Token::TokenKind Kind);
};
#endif
```
Except for the constructor, the public interface has only the next() method, which returns the next token. The method acts like an iterator, always advancing to the next available token.

5. Let’s implement the Lexer class in the `Lexer.cpp` file. It begins with some helper functions to classify characters:
```
#include "Lexer.h"
namespace charinfo {
LLVM_READNONE inline bool isWhitespace(char c) {
	return c == ' ' || c == '\t' || c == '\f' ||
		c == '\v' ||
	c == '\r' || c == '\n';
}
LLVM_READNONE inline bool isDigit(char c) {
	return c >= '0' && c <= '9';
}
LLVM_READNONE inline bool isLetter(char c) {
	return (c >= 'a' && c <= 'z') ||
		(c >= 'A' && c <= 'Z');
}
}
```

6. From the grammar in the previous section, we know all the tokens of the language. But the grammar does not define the characters that should be ignored. For example, a space or newline character adds only whitespace and are often ignored. The next() method begins with ignoring these characters:
```
void Lexer::next(Token &token) {
	while (*BufferPtr &&
		charinfo::isWhitespace(*BufferPtr)) {
	++BufferPtr;
}
```

7. Next, make sure that there are still characters left to process:
```
if (!*BufferPtr) {
	token.Kind = Token::eoi;
	return;
}
```

8. We first check whether the character is lowercase or uppercase. In this case, the token is either an identifier or the with keyword, because the regular expression for the identifier also matches the keyword.
```

```