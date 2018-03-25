# MCNP Algorithms

## Fixed-source particle histories

This procedure describes the tracking of a neutron history in an MCNP run. 

1. History overhead
	* Random number sequence is set up.
	* History number (NPS) is set.
	* Particle type (IPT) is set (1=n,2=p,3=e).
	* Arrays/variables are initialized (as 0).
	* History branch (NODE) is set.
1. Source routine is called.
	* Source type is set (fixed sources, surface source, criticality source, user-defined source).
	* Source parameters are set (position, direction, energy, weight, time, starting cell).
1. Checks made; book-keeping started/inital tallies are created.  
1. **Transport:** For neutrons, the distance to next encountered surface is calculated. (this is the minimum positive distance to any boundary).
	1. Total cross sections are found from library.
	1. The distance to the next collision is sampled.
	1. Track length of particle is found as the minimum of the distance to the next boundary or next collision.
	1. Track length tally is collected.
	1. Particle information (time, position, energy) updated.  
1. **Boundary:** If the minimum track length corresponds to a boundary, particle is transported there, surface tallies are processed, particle distance traveled is processed as going into the next cell. Repeat _transport_.  

1. **Collision:** If distance to collision is less than distance to surface:
	1. Sample the collision (nuclide involved, collision type, target nuclide velocity).
	1. Generate new particles/parameters as necessary. Repeat _transport_.

Histories include everything that happens after the generation of a particle–all collisions, progeny, etc. Tallies are tracked by history, and upon history termination (capture, or variance reduction) are added to total.


## Criticality calculations

The procedure is cyclic for criticality calculations, since iterations must occur to determine $k_{\textit{eff}}$.

1. User supplies data:
	* Nominal number of histories ($N$) per cycle.
	* Initial guess of $k_{\textit{eff}}$.
	* Number of cycles, $I_c$, to skip before accumulation of $k_{\textit{eff}}$.
	* Total number of cycles, $I_t$, in the problem.  
1. **Cycle:** Random $M$ particles are started per cycle (total source weight is $N$, and so each particle weight is $N/M$).
1. Execute _transport_, _boundary_, and _collision_ procedures as defined above. Exceptions are:
	* If fission is possible, estimate $k_{\textit{eff}}$.
	* Fission is treated as capture; fission sites are saved for next cycle source.
	* Reaction is sampled (fission can't occur $\rightarrow$ it was treated as absorption)  
Repeat _Cycle_
	
	
	
	
