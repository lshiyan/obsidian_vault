https://arxiv.org/pdf/2605.08426 Don't really understand the theory in this paper.

- MAIN IDEA: Mechanism design is insufficient in order to guarantee globally optimal results, we must explicitly design agents prosocially in order to take into account the welfare of others.
- Mechanism design assumes that all relevant variables can be specified and enforced, but this is not always the case, as uncertainty exists in real world environments.
- An *incontractible cell* is a set of future states that a mechanism cannot distinguish efficiently, even though the maximum welfare action differs among them.
- An example is the following game: Here, even if contracts explicitly prevent defection, rational agents will still converge on the suboptimal choice in red. However, prosocial agents, which take into account the welfare of others, will converge on the optimal green choice.
![[Pasted image 20260817115241.png]]
- The prosocial agents want to maximize $V_i^{\lambda} (\bar{a}, \omega) = u_i(\bar{a}, \omega) + \lambda W(\bar{a}, \omega)$. The first and second terms denote the individual agents payoff ($u_i$ is the utility function for a given action and current state $\omega$), and the global welfare, which is just a sum of the individual utilities.
- They define a mechanism as a map from a specific partition of states. I.e. if there are three states $\omega_{1,2,3}$ , a partition could be grouping $\{\omega_1, \omega_2\},\{\omega_3\}$. The mechanism would then act on the specific partitions, but cannot distinguish between states in the same partition.