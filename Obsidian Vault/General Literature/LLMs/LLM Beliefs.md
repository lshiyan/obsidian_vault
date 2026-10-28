https://aclanthology.org/2026.acl-long.1905.pdf

- MAIN IDEA: LLM intermediate states show good evidence of belief tracking across various axis of belief.
- It has been found that unsupervised learning can reveal latent space directions that are associated with truth in LLMs.
- They score LLM activations along 4 axis, corresponding to different aspects of belief:
	- Accuracy, how much intermediate representations separate true from false statements.
	- Use, steering a models activations in the truth direction will directly change the logit distribution.
	- Coherence, if an agent believes in $p$, they should not believe in $\neg p$. Logical rewordings should fall in the same truth partition.
	- Uniformity, the direction associated with "truth" should be the same across multiple domains.
- For the accuracy experiment, they probe the models using linear classifiers. They find that instruction fine tuned models exhibit heads that are more accurate to probing than non-IFT models.
- For the use experiment, they steer activations along the direction associated with the mass-mean $\theta_{act} = \mu_{act}^+ - \mu_{act}^-$. They use metrics $E$ and $\vec{E}$ to measure the absolute effect of intervention and the direction-specific effect respectively. High $\vec{E}$ and low $E$ represents a very specific directional effect.
- In the coherence experiment, they measure the model's accuracy in satisfying basic probabilistic principles, such as negation summing to 1 and conjunction / disjunction.
- In the uniformity experiment, they find that larger diverse datasets allow models to generalize across different domains.
- It seems that IFT models are better at representing truth than their counterparts. 
- Attention heads seem to have the most robust truth representations. Residual streams are aggregations of multiple attention heads, and as such may have a higher variance than a specific head.