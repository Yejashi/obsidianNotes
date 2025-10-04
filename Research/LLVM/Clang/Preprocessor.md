For C-family programming languages, preprocessing is an early compilation phase that replaces any directive starting with a hash (#) character—#include and  # define, to name but a few—with some other textual contents (or non- textual tokens, in some rare cases).

For example, the preprocessor will basically copy and paste contents of header files designated by the # include directive into the current compilation unit before parsing it.

The `-E` command-line option for clang is pretty useful for printing textual content right after preprocessing

### Working with SourceLocation and SourceManager
When working closely with source files, one of the most fundamental questions is how a compiler frontend would be able to locate a piece of string in the file.

On one hand, printing format messages well (compilation error and warning messages, for example) is a crucial job, in which accurate line and column numbers must be displayed. On the other hand, the frontend might need to manage multiple files at a time and access their in-memory content in an efficient way

 In Clang, these questions are primarily handled by two classes: `SourceLocation` and
`SourceManager`. 

#### SourceLocation Class
The **SourceLocation** class is used for representing the location of a piece of code in its file.

When it comes to its implementation, using line and column numbers is probably the most intuitive way to do this. However, things might get complicated in real-world scenarios, such that internally, we can't naively use a pair of numbers as the in-memory representations for source code locations

One of the main reasons is that SourceLocation instances are extensively used in Clang's code base and basically live through the entire frontend compilation pipeline. 

Therefore, it's important to use a concise way to store its information rather than two 32-bit integers (and this might not even be sufficient since we also want to know the origin file!), which can easily bloat Clang's runtime-memory footprint.

Clang solves this problem by using the elegantly designed SourceLocation as the pointer (or a handle) to a large data buffer that stores all the real source code contents such that SourceLocation only uses a single unsigned integer under the hood, which also means its instances are trivially copyable—a property that can yield some performance benefits.

Since SourceLocation is merely a pointer, it will only be meaningful and useful when put side by side with the data buffer we just mentioned, which is managed by the second main character in this story, **SourceManager**.

#### SourceManager Class
The SourceManager class manages all of the source files stored inside the memory and provides interfaces to access them.

It also provides APIs to deal with source code locations, via SourceLocation instances we just introduced. For example, to get the line and column number from a SourceLocation instance, run the following code:
```
void foo(SourceManager &SM, SourceLocation SLoc) {
   auto Line = SM.getSpellingLineNumber(SLoc),
   Column = SM.getSpellingColumnNumber(SLoc);
   …
}
```

The Line and Column variables in the preceding code snippet are the line and column number of the source location pointed by SLoc, respectively.

You might wonder why we are using the term `spellingLineNumber` instead of just `LineNumber` in the preceding code snippet. It turns out that in the cases of macro expansion (or any expansion happening during preprocessing), Clang keeps track of the macro content's `SourceLocation` instance before and after the expansion.

### Preprocessor and Lexer Essentials
The roles and primary actions performed by Clang's **preprocessor** and lexer, **represented** by the Preprocessor and Lexer classes respectively, are illustrated in the following diagram:

![[Pasted image 20251004163931.png]]

A **token** is a substring from the original source code that acts as the minimum building block for semantic reasoning.

 In some of the traditional compilers, the lexer is responsible for chopping the input source code into a sequence of tokens or a token stream, as shown in the preceding diagram. This token stream will later be fed into the parser to construct the semantic structure.

Implementation-wise, Clang takes a slightly different path from traditional compilers (or those from textbooks): **Lexer**, employed by **Preprocessor**, is still the primary performer to cut source code into tokens.

However,  Lexer keeps its hands off whenever encountering a preprocessor directive (that is, anything that starts with a #) or a symbol, and relays that task to either the macro expansion, the header file resolver, or pragma handlers that are organized by the **Preprocessor**. 

These assisting components inject extra tokens, if needed, into the main token stream, which would eventually be returned back to the user of Preprocessor.

In other words, most consumers of the token stream don't directly interact with Lexer, but with the Preprocessor instances

This makes people call the Lexer class a raw lexer (as shown in the previous diagram), since Lexer by itself only generates a token stream that hasn't been preprocessed.

To give you a more concrete idea of how to use Preprocessor to retrieve a token (stream), the following simple code snippet has been provided. This shows a way to get the next token from the source code currently processing it:
```
Token GetNextToken(Preprocessor &PP) {
   Token Tok;
   PP.Lex(Tok);
   return Tok;
}
```

Token here is the class representing a single token in Clang.

#### Understanding Token
The Token class is the representation of a single token, either from the source code or a virtual one that served a special purpose

For the Token class, there are two things we want to highlight here, as follows:
1. **Token kind** tells you what this token is.A
2. **Identifier** represents both language keywords and arbitrary frontend tokens (a function name, for example). Clang's preprocessor used a dedicated IdentifierInfo class to carry extra identifier information, which we're going to cover later in this section.


