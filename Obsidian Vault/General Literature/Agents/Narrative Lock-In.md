https://openreview.net/pdf?id=V9fKxgIebr This paper is kinda trash lmao

- MAIN IDEA: To solve the issue of confirmation bias in LLM agents, we need independent supervision.
- LLM agents struggle with multi-source, multi-step tasks, essentially more realistic tasks. Early erroneous claims can shape downstream task behavior negatively, and new evidence will only be used to further the claim through confirmation bias. 
- Existing harnesses have memory, reflection, critic modules that are interpreted by the execution agent, which is already suffering from this confirmation bias instead of producing corrective behavior.
- Narrative Lock-In is the tendency during task execution to mistake narrative for ground truth. Formally, if $n_k$ denotes a narrative around claim $c_k$, and $E_{\lt T}$ denotes all the evidence up to the current time $T$, then narrative lock-in occurs when some claim $c_{\tau}$, with $\tau \lt\lt T$, is consistent with current evidence, and as such such actions and plans are constrained by the narrative. When new evidence arrives, the claim is not revised, rather the new evidence is assimilated into the claim $c_{\tau}$ 
- The experiments have multiple models being given claims across a variety of domains, and then challenged as they make conclusions. Across all types of challenges, lock-in, (as measured by TF-IDF across adjacent response pairs), occurs substantially, and evidence-based challenges don't really mitigate this.
- They propose Nexus, which decouples execution from supervision, in order to solve this. Nexus is made of 3 components: 
	- 1. Observer: Makes concrete observations from the executor's trace.
	- 2. WorldMap: Uses the Observer's observations to maintain a structured task state object. They inject this object into the executor's prompt at each point.
	- 3. Mentor: Detects claim-evidence mismatches and triggers intervention when lock-in occurs.