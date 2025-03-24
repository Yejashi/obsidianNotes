Fluxion will not scale forever because of its design and the way it does traversals (DFS).
- scaling limitation towards the end of the Fractale project

Constraint satisfaction for milp problems, flux is not going to work well.
- Use graph NN to repro the matching process in fluxon.
- Risk: amount time it would take to implement

Proposal
- see whether we can apply a graph NN to approximate fluxion matches for a simple graph without consideration of time.
	- Describe fluxion and how dfs works within fluxion
	- Model the same resource graph (node, cores, sockets, gpus)
	- Perform subgraph isomporhism with a graph NN approch on that graph
		- see whether we can return a similar or ideally idenital mathch with what fulixion coems up with.

Basically
- compare match allocatied output for a resource query to the output of the network
	- fixed resource graph and small job set

Try it on a really small resource graph first.