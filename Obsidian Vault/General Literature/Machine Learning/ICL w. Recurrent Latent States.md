https://arxiv.org/pdf/2608.09888

- MAIN IDEA: We do not need CoT prompting for ICL, instead we can use a latent state that is updated using new information from each training example. 
- In-context learning (ICL) is where you present a model with examples at inference time (few-show  / one-shot learning is an example).
- Latent reasoning is an alternative to chain of thought prompting, where a model continuously transforms its own hidden state and then only decodes the final answer, removing natural language tokens as intermediate computation.
- Given a task that provides demonstrations $\{(x_t, y_t)\}_{t=1}^K$, the model processes elements sequentially into a latent state $S_t = U_{\theta}(S_{t-1}, D_t)$, where $D_t$ is the content on the $t$-th demonstration. This means that information from previous demonstrations are used to inform the information from later ones, and this recurrent context is similar to the attention mechanism in Transformer models.
- After receiving their contextual latent state, the query vector $x^*$ is transformed in a latent workspace $H_r$, using the following equations. Conceptually $S_t$ is what supports in-context learning, as it changes as evidence is encountered. $H_r$ represents ongoing computation and is what supports the idea of latent representations.
	![[Pasted image 20260819141306.png]]
- 