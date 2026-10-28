https://arxiv.org/pdf/2605.15343

- MAIN IDEA: It is important to determine exactly where shifts in belief originate from in LLMs.
- It is not clear in LLMs what evidence actually motivates a shift in opinion. 
- ![[Pasted image 20260923144152.png]]
- The BE uses 5 distinct modules: 
  1. Argument Extractor: An independent LLM takes in each message $m_t$ and extracts candidate messages $\tilde{E}_t = J(m_t) = \left\{ \tilde{e}_i = (c_i, p_i, r_i) \right\}_{i=1}^{n_t}$. The $c_i$ are claims made in the message, the $p_i$ are the polarity of the claim, a binary value, and the $r_i$ is the originator of the claim, either seed, you, or the opponent.
  2. Judge: Each claim receives a separate score $s_i$ from either an LLM judge or a classifier fine tuned on argument quality pairs. Same polarity arguments are then run through a similarity search with previous arguments to determine if they are duplicates or not. 
  3. Structured Memory: Each claim is stored as an $ArgumentRecord$ with its various parameters. Both active and inactive claims are stored, but only active claims can affect belief.
  4. Update: Given the active set $A_t$, we compute the belief score as follows: 
     $L_t = \sum_{i \in A_t} p_i \ln(1 + s_i \gamma_i)$, $S_t = 2\sigma(L_t) - 1 = \frac{2}{1 + \exp(-L_t)} - 1$. 
	 (This is very sus lmao)
  5. Response: We finally generate a response using an instruction based on the value of $S_t$, strong claims $R_t$, and a sequence of recent history $h_t$. 