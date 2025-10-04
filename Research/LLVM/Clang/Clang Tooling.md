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
- `FrontendAction::BeginSourceFileAction(…)/EndSourceFileAction(...)`:
	- These are callbacks that derived classes can override to perform actions right before processing a source file and once it has been processed, respectively.
- `FrontendAction::ExecuteAction(…)`:
	- This callback describes the main actions to do for this FrontendAction. 
	-  Note that while no one stops you from overriding this method directly, many of FrontendAction's derived classes already provide simpler interfaces to describe some common tasks. For example, if you want to process an AST, you should inherit from ASTFrontendAction instead and leverage its infrastructures.
- `FrontendAction::CreateASTConsumer(…)`:
	- This is a factory function that's used to create an **ASTConsumer** instance, which is a group of callbacks that will be invoked by the frontend when it's traversing different parts of the AST (for example, a callback to be called when the frontend encounters a group of declarations).

### Clang Plugins
A Clang plugin allows you to dynamically register a new **FrontendAction** (more specifically, an ASTFrontendAction) **that** can process the AST either before or after, or even replace, the main action of **clang**.

A plugin can be easily loaded into a normal clang by using simple command-line options:
```
$ clang -fplugin=/path/to/MyPlugin.so … foo.cpp
```

However, the biggest downside of using the Clang plugin is its API issue. In theory, you can load and run your plugin in any clang executable, but only if the C++ APIs (and the ABI) are used by your plugin and the clang executable matches it.

Unfortunately, for now, Clang (and also the whole LLVM project) has no intention to make any of its C++ APIs stable. In other words, to take the safest path, you need to make sure both your plugin and clang are using the exact same (major) version of LLVM.

### LibTooling and Clang Tools
**LibTooling** is a library that provides features for building standalone tools on top of Clang's techniques.

You can use it like a normal library in your project, without having any dependencies on the clang executable. Also, the APIs are designed to be more high-level so that you don't need to deal with many of Clang's internal details, making it more friendly to non-Clang developers.

A **Language server** is one of the most famous use cases of libTooling. A Language server is launched as a daemon process and accepts requests from editors or IDEs. These requests can be as simple as syntax checking a code snippet or complicated tasks such as code completions.

While a Language server does not need to compile the incoming source code into native code as normal compilers do, it needs a way to parse and analyze that code, which is non-trivial to build from scratch. libTooling avoids the need to recreate the wheels in this case by taking Clang's techniques off-the-shelf and providing an easier interface for Language server developers.

To give you a more concrete idea of how libTooling differs from the Clang plugin, here is a (simplified) code snippet for executing a custom **ASTFrontendAction** called **MyCustomAction**:
```
int main(int argc, char** argv) {
 CommonOptionsParser OptionsParser(argc, argv,…);
 ClangTool Tool(OptionsParser.getCompilations(),
   {"foo.cpp"});
 return Tool.run(newFrontendActionFactory<MyCustomAction>(). get());
}
```

As shown in the previous code, you can't just embed this code into any code base. libTooling also provides lots of nice utilities, such as CommonOptionsParser, which parses textual command-line options and transforms them into Clang options for you.

#### Clang Tools
