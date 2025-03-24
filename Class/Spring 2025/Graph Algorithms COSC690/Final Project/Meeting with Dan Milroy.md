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
- 10 nodes, 18 cores each
- couple of job specifications

If we can make progress on this, then we can scale it up.

What would not be acceptable
- moltiple matches for the sam resources
- Job one node A, all
	- If request 2 cant mape to also node a
	- Need to encode strong constraints.

Just to reiterate
- How do you introduce hard constraitns in GNN's?
	- Used in drug discovery all the time, reference
	- Maybe encode the output and try to submit that to an actual flux instance ans see if that queues?

Back to motivation
- Will run into scaling problem with fluxion
- Fractale project
	- Multi cluster scheduling, we'll eventually run into a scaling problem with the current fluxion (low throgphout)