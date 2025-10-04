There are currently three kinds of tooling and extension options available in Clang: **Clang plugins**, **libTooling**, and **Clang Tools**.

To explain their differences and provide more background knowledge when we talk about Clang extensions, we need to start from an important data type first: the **clang::FrontendAction class**.


### The FrontendAction class
We went through a variety of Clang's frontend components, such as the preprocessor and Sema, to name a few.

Many of these important components are encapsulated by a single data type, called **FrontendAction**.

A **FrontendAction** instance can be treated as a single task running inside the frontend.


