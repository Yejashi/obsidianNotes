There are currently three kinds of tooling and extension options available in Clang: **Clang plugins**, **libTooling**, and **Clang Tools**.

To explain their differences and provide more background knowledge when we talk about Clang extensions, we need to start from an important data type first: the **clang::FrontendAction class**.
### The FrontendAction class
We went through a variety of Clang's frontend components, such as the preprocessor and Sema, to name a few.

Many of these important components are encapsulated by a single data type, called **FrontendAction**.

A **FrontendAction** instance can be treated as a single task running inside the frontend.

It provides a unified interface for the task to consume and interact with various resources, such as input source files and ASTs, which is similar to the role of an **LLVM Pass** from this perspective (an LLVM Pass provides a unified interface to process LLVM IR).


However, there are some significant differences with an LLVM Pass:
- Not all of the frontend components are encapsulated into a **FrontendAction**, such as the parser and Sema. They are standalone components that generate materials (for example, the AST) for other FrontendActions to run.
- Except for a few scenarios (the Clang plugin is one of them), a Clang compilation instance rarely runs multiple FrontendActions. Normally, only one FrontendAction will be executed.

Generally speaking, a FrontendAction describes the task to be done at one or two important places in the frontend.

This explains why it's so important for tooling or extension development – we're basically building our logic into a FrontendAction (one of FrontendAction's derived classes, to be more precise) instance to control and customize the behavior of a normal Clang compilation.

To give you a feel for the FrontendAction module, here are some of its important APIs:
- 