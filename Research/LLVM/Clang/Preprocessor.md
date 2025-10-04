For C-family programming languages, preprocessing is an early compilation phase that replaces any directive starting with a hash (#) character—#include and  # define, to name but a few—with some other textual contents (or non- textual tokens, in some rare cases).

For example, the preprocessor will basically copy and paste contents of header files designated by the # include directive into the current compilation unit before parsing it.

The `-E` command-line option for clang is pretty useful for printing textual content right after preprocessing

### Working with SourceLocation and SourceManager

