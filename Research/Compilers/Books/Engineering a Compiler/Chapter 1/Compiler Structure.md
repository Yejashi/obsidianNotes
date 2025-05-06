As the single-box model suggests, a compiler must both understand the source program that it takes as input and map its functionality to the target machine. 

The distinct nature of these two tasks suggests a division of labor and leads to a design that decomposes compilation into two major pieces: a front end and a back end.

![[Pasted image 20250506114036.png]]

The front end focuses on understanding the source-language program.  The back end focuses on mapping programs to the target machine. This separation of concerns has several important implications for the design and implementation of compilers.

The front end must encode its knowledge of the source program in some structure for later use by the back end.

