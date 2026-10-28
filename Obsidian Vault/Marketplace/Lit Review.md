
Agent Protocol Survey (http://arxiv.org/abs/2505.02279): 
	1. Function calling: LLM's output JSON corresponding to a predefined API endpoint, must supply beforehand. Static definitions, cannot dynamically discover new tools. Security is also ad-hoc, need protocol level standards.
	2. MCP: Client applications serves as initiator of interactions with MCP servers. MCP servers provide data, services, and interaction templates to enrich the client application.
		1. Tools: Allow LLMs to invoke external APIs
		2. Resources: Application controlled data, databases or documents for example.
		3. Prompts: User controlled templates for consistent input.
		4. Sampling: Server controlled, generated LLM completions to the client.
		Security Vulns: 
		![[Pasted image 20260630104722.png|625]]
	3. A2A: Client agents work on requests on behalf of users, discovers remote agents through AgentCards.
		1. Client Agents: Responsible for understanding user's requests, and Task Initiation. Creating a structured Task object to send to remote agents, tasks are *stateful*, so can be updated via SSE events.
		2. Agent Cards: JSON document that specifies an agent's metadata, specifically supported skills. Remote agents need Agent Cards in order to be visible in the A2A architecture.
		3. Skills: An agent's capabilities, described by a name, description, input parameters, and output format. Skills are invoked via Tasks.
		4. Tasks: Atomic unit of work. Specifies skill to be executed. 
		5. Artifacts: Outputs of skill execution, structured outputs, computed results, documents, which are transmitted back to client agent.
   Scaling MAS (http://arxiv.org/abs/2512.08296):
	-  Agentic tasks are those requiring: 
		1. Sustained multi-step interactions with an environment
		2. Iterative information gathering under partial observability (You do not know everything that is happening in the environment.)
		3. Adaptive strategy refinement based off of environmental feedback.
		Based off of this, agentic benchmarks must include sequential interdependence, where actions depend on earlier observations, so one-shot cannot work. Partial observability, such that information must be hidden behind tool use or querying. Adaptive strategy, the policy LLM must update its beliefs based on new evidence obtained through environmental interactions.
	- Existing MAS are generally tested on datasets that are fundamentally non-agentic like HumanEval, (no partial observability), so they do not fit the framework they are applied to.
	- Single agent systems (SAS) maximize context integration by providing a unified memory stream where all reasoning steps have full access to history. MAS do not have this, since there is always a coordination tax between different agents.
	- There is limited research on how architectural choices shape coordination costs.
	- Decentralized coordination is good when we need parallel exploration of large search spaces
	- MAS topologies: 
		![[Pasted image 20260703111024.png|625]]
	- MAS mechnics: 
	 ![[Pasted image 20260703112859.png|657]]
   MAS Orchestration (https://arxiv.org/pdf/2601.13671):
   - ![[Pasted image 20260703132547.png|662]]
Collusion in Cournot Games: https://arxiv.org/pdf/2410.00031
- $n$ firms with $m$ commodities, the quantity $q_{i,j}$ denotes the quantity of $\gamma_j$ that the firm $f_i$ produces. The linear inverse demand function is given by $p_j(Q_j) = \alpha_j - \frac{Q_j}{\beta_j}$ . The alpha and beta terms are positive real numbers, and $Q_j = \sum_{i=1}^nq_{i,j}$ . (As quantity goes up, price goes down.) The marginal cost per unit is denoted by $c_{i,j}$. After the end of each round, each firm receives a profit $\prod^i(s) = \sum_{j=1}^m (p_j(s) - c_{i,j}) q_{i,j}$. $s$ represents the total strategy profile of each firm $s = (s_1, s_2 ...)$, where each strategy is a quantity $s_i = (q_{i,1}, q_{i,2} ...)$. Basically the strategy is how much of each commodity the firm chooses to produce. The price is the linear inverse demand function for that particular commodity, formulated by the strategy of all firms that round.
- We quantify collusion using consumer surplus, which represents the benefit obtained by consumers when they pay less for a product than the maximum amount that they are willing to pay. The expression is $\sum_{j}^{m}(\frac{1}{2}(\alpha_j - p_j)\sum_{i=1}^{n}q_i)$. This represents the surplus by the consumer, the alpha - p_j term, multiplied by the quantity demanded for each commodity.
- Shows that collusion increases across multiple LLMs / experiments.
Collusion Position Paper: https://openreview.net/pdf?id=Vhi9tHbKTa
- Bertrand games differ from Cournot games in that in Bertrand games, *demand* is fixed and prices determine quantity sold, whereas in Cournot games, *prices* are fixed and the quantity that a firm produces determines how much is sold.
- In Bertrand games with a logit demand model, the demand $q_i$ for a given firm's product, based on the price of $p_i$, is given by: 
	![[Pasted image 20260717103712.png]]
	The parameters $\mu$ and $a_i$ are meant to capture the horizontal and vertical differentiation between products, and $a_o$ the outside option. Horizontal differentiation refers to different consumers simply having different tastes (temperature flattens out the distribution), while vertical differentiation refers to products being superior to each other (biases the exponents).
- The profit of the i-th firm can be calculated as $\pi_i = (p_i - \alpha c_i)q_i$, and we can calculate the Nash equilibrium of this as $\frac{\partial \pi_i}{\partial p_i} = 0$ . Any profits that are above this Nash solution can be thought of as supra-competitive. At the monopoly equilibria, the $p_i$ will jointly optimize the total profit $\sum_i (p_i - \alpha c_i)q_i$ , and the metric of collusion can be defined as the average profit gain $\Delta = \frac{\widetilde{\pi} - \pi^N}{\pi^M - \pi^N}$ , where $\tilde{\pi}, \pi^M , \pi^N$ are the per firm profit, per firm profit at Nash equilibria, and per firm profit at monopoly equilibria respectively.
Selling Algorithms Paper: https://www.tse-fr.eu/sites/default/files/TSE/documents/doc/wp/2020/wp_tse_1146.pdf
- There are $n$ firms that sell a singular product on the marketplace, all have a constant marginal cost $c \gt 0$. For each period $t$, the firms observe all past prices and sets a price for the current period. Each period, the platform displays a subset $N_t$ of products, and each firm in that subset receives standard logit demand. Consumer surplus (expected value of the maximum utility) is defined as: ![[Pasted image 20260721115742.png]]
- PDP (Price directed prominence) is where only the $k$ firms with the lowest price are displayed. Dynamic PDP rewards firms for keeping prices low to prevent collusion.
Recommender System Interventions: https://arxiv.org/pdf/2309.14548
- The 3 key elements of the algorithmic pricing game are: 
	1. The consumer demand model, canonically using the logit model.
	2. The pricing algorithms themselves, where sellers use basic Q-learning algorithms.
	3. The game sequence, where at each timestep sellers simultaneously make pricing decisions.
- Two types of recommenders: 
	1. Revenue-maximizing recommender: For each customer i, it generates a list of recommendations in order to maximize the revenue that the businesses receive.
	2. Utility-maximizing recommender: The recommendations generated are generated explicitly to maximize the utility from customers.
AgenticPay: https://arxiv.org/pdf/2602.06008
- We have an open market with buyers and sellers, and each entity has access to private internal constraints that it uses to decide which business to undertake. Each seller sells a product / service that is represented with a feature vector, and the transactions take place under a shared market context. Each negotiation is a finite horizon conversation, messages are generated using a policy conditioned on any shared information and the prior conversation history, and a parser turns messages into actions.
- Examples of tasks under the AgenticPay framework.![[Pasted image 20261026134138.png]]
- Frontier-models are generally much stronger at providing both seller and buyer surplus than open-weight models.