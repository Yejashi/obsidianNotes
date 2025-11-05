### Things to Know
- Syntax Analysis
	- Bottom-Up Parsing
		- LR parsing algorithm
		- Construct LR(0) sets of items for grammar
		- Construct SLR parsing table
		- Construct LR(1) sets of items for grammar
		- Construct canonical parsing table
	- Error Handling
		- Different error recovery strategies
- Intermediate Code generation
	- Draw DAG
	- Three address code
	- Translate statement with backpatching
	- Translate statement without backpatching
	- Translating switch statements
### Syntax Analysis

#### Calculating FIRST and FOLLOW
What do they both mean?
- FIRST(X) = "What could appear first if i start expanding X?"
- FOLLOW(X) = "What could appear right after X in a valid sentence?"


