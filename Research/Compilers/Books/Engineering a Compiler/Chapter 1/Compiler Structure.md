As the single-box model suggests, a compiler must both understand the source program that it takes as input and map its functionality to the target machine. 

The distinct nature of these two tasks suggests a division of labor and leads to a design that decomposes compilation into two major pieces: a front end and a back end.

![[Pasted image 20250506114036.png]]

The front end focuses on understanding the source-language program.  The back end focuses on mapping programs to the target machine. This separation of concerns has several important implications for the design and implementation of compilers.

The front end must encode its knowledge of the source program in some structure for later use by the back end. This **intermediate representation** (IR) becomes the compiler's definitive representation for the code it's translating.

At each point in compilation, the compiler will have a **definitive representation**. It may, in fact, use several different irs as compilation progresses, but **at each point, one representation will be the definitive ir**. We think of the definitive ir as the version of the program passed between independent phases of the compiler, like the ir passed from the front end to the back end in the preceding drawing.

