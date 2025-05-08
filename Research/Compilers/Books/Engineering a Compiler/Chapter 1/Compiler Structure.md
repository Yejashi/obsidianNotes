As the single-box model suggests, a compiler must both understand the source program that it takes as input and map its functionality to the target machine. 

The distinct nature of these two tasks suggests a division of labor and leads to a design that decomposes compilation into two major pieces: a front end and a back end.

![[Pasted image 20250506114036.png]]

The front end focuses on understanding the source-language program.  The back end focuses on mapping programs to the target machine. This separation of concerns has several important implications for the design and implementation of compilers.

The front end must encode its knowledge of the source program in some structure for later use by the back end. This **intermediate representation** (IR) becomes the compiler's definitive representation for the code it's translating.

At each point in compilation, the compiler will have a **definitive representation**. It may, in fact, use several different irs as compilation progresses, but **at each point, one representation will be the definitive ir**. We think of the definitive ir as the **version of the program passed between independent phases of the compiler**, like the ir passed **from the front end to the back end** in the preceding drawing.

***

Introducing an IR makes it possible to add more phases to compilation. The compiler writer can insert a third phase between the front end and the back end. This middle section, or **optimizer**, takes an IR program as its input and produces a semantically equivalent IR program as its output. By using the IR as an interface, the compiler writer can insert this third phase with minimal disruption to the front end and back end. This leads to the following compiler structure, termed a **three‐phase compiler**.

![[Pasted image 20250506152916.png]]

The optimizer is an ir-to-ir transformer that tries to improve the ir program in some way. The optimizer can make one or more passes over the ir, analyze the ir, and rewrite the ir. 

***

In practice, the conceptual division of a compiler into three phases, a front end, a middle section or optimizer, and a back end, is useful. The problems addressed by these phases are different. The front end is concerned with understanding the source program and recording the results of its analysis into ir form. The optimizer section focuses on improving the ir form. The back end must map the transformed ir program onto the bounded resources of the target machine in a way that leads to efficient use of those resources.

![[Pasted image 20250506155150.png]]



