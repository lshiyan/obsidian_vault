https://arxiv.org/pdf/2602.11583

- The formal object of MARL is what is called a decentralized partially observable Markov decision process: $D = \langle S, A, P, \Omega, O, I, n, R, \gamma, f \rangle$.
	1. $I$ is the set of agents
	2. $S$ is a joint state space
	3. $A = A_1 \times A_2 ...$ is the joint action space, and $a$ is an instance of this space
	4. $P = P(s' | s, a)$ is the joint transition space
	5. $\Omega$ is the observation space (Note that this is different than the full state space due to partial observability.)
	6. $O = O(s, i): S \times I \rightarrow \Omega$ is a function that takes in the state and an agent and maps to a distribution over observations.
	7. $R = R(s,a)$ is the reward function.
	8.  $\gamma$ is the discount factor.
- In this setting, communication can be thought of as an additional action step. At each time step $i$, each agent generates a message $m_i$ based on their observation and internal state. Agents aggregate messages into a context vector $c_i$, and produces their next actions as a function of their current observations and context vectors $a_i = a_i(o_i, c_i)$.
- In large environments, the individual observation of each agent is typically only a small portion of the global state. As such, it is necessary to design communication protocols that can exchange task-relevant information while still remaining compact.
- Stable communication strategies are also difficult, as in many environments the dynamics of the environment might change as agents acquire new information.
- Communication makes it difficult to properly assign credit to individual agents, as now there is a dependence on the information that they choose to give out.
- Learned communication protocols may lack interpretability as opposed to natural language communication.