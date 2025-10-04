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

