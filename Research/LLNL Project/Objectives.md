In a single sentence the objective of this endeavor is to track and report the behavior of optimization passes during compilation.

Initial Objectives: For each function, extract how many transformation passes:
- Were attempted
- Succeeded
- Failed

What needs to be tracked:
- Transformations attempted
	- This includes all optimization attempts (i.e loop unrolling, inlining, dead code elimination, etc)
- Transformations Failed
	- This should happen when a transformation is skipped or doesn't apply (i.e a loop is not unrolled for `x` reason.)
- Transformation Succeeded
	- This happens when a particular transformation successfully modifies the IR.
Q
### What is needed to achieve this?
This project doesn't directly fit into the usual categories of transformation or analysis passes. 

However, it seems that LLVM's modular structure and its pass management system allow for such meta-level tracking.

To even attempt this, i need to:
- Familiarize myself with the new Pass Manager (NPM), as LLVM deprecated the legacy Pass Manager.
- Learn how passes interact, including their dependencies and how analysis results are preserved.

Where to Integrate?
- **At the Pass Manager Level**: This involves hooking into the Pass Manager to observe all passes applied globally or per function.
- **Within a Custom Pass**: This involves running after the -O3 pipeline and retroactively collecting metadata about transformations.




### Potential Workflow

The potential workflow of getting the data to thicket goes as follows:
- For each translation unit/module, output a file that includes all the remark information along with the location.
- Run the application and store the `cali` file containing the CCT.
	- Make sure to output the lines that correspond to the regions.
- Create a reader that maps the lines to the region.


Steps:
- Build entire call path for every function
- When a remark tells me the location, add to the metadata of the current module call path
- Example:
	- proxy.cpp: main->wrapper->foo[file1.cpp]
	- file1.cpp: foo->bar->loop
	- file2.cpp: foo->foobar
	- Remarks
		- loop-vectorize: in bar at file1.cpp
	- Merging:
		- main->wrapper->