Source: [Anywhere, Any-Time Binary Instrumentation](https://dl.acm.org/doi/pdf/10.1145/2024569.2024572)

### Abstract
```txt
The Dyninst binary instrumentation and analysis framework
distinguishes itself from other binary instrumentation tools
through its abstract, machine independent interface; its em-
phasis on anywhere, any-time binary instrumentation; and
its low overhead that is proportional to the number of in-
strumented locations. Dyninst represents the program in
terms of familiar control flow structures such as functions,
loops, and basic blocks, and users manipulate these repre-
sentations to insert instrumentation anywhere in the binary.
We use graph transformation techniques to insure that this
instrumentation executes when desired even when instru-
menting highly optimized (or malicious) code that other in-
strumenters cannot correctly instrument. Unlike other bi-
nary instrumenters, Dyninst can instrument at any time in
the execution continuum, from static instrumentation (bi-
nary rewriting) to instrumenting actively executing code
(dynamic instrumentation). Furthermore, we allow users
to modify or remove instrumentation at any time, with such
modifications taking immediate effect. Our analysis tech-
niques allow us to insert new code without modifying unin-
strumented code; as a result, all uninstrumented code exe-
cutes at native speed. We demonstrate that our techniques
provide this collection of capabilities while imposing similar
or lower overhead than other widely used instrumenters.
```

**Key Features of Dyninst**
- **Abstract, Machine-Independent Interface**: Unlike tools tied to specific architectures, Dyninst offers a general interface that works across various machine types.
- **Anywhere, Any-Time Instrumentation**: It can add or modify instrumentation (additional code to analyze or monitor a program) at virtually any point in a program's execution life cycle.
- **Low Overhead**: The performance impact is proportional to the amount of instrumentation added, meaning uninstrumented parts of the program run at native speed.

**Program Representation**
- Dyninst represents a program in terms of familiar structures like **functions**, **loops**, and **basic blocks** (units of code with a single entry and exit point).
- Users can interact with these structures to insert or modify instrumentation code.



