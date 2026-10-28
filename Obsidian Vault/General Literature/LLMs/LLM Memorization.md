https://arxiv.org/pdf/2505.24832

- MAIN IDEA: It is important to distinguish between unintended memorization of a dataset versus generalization.
- It is an open question as to what extent LLMs actually memorize their inputs, and to what extent they generalize. Simply outputting a given string is not enough to say that it has memorized it.
- Define memorization when the input can be compressed into a shorter encoding when the model is available. 
- *Unintended* memorization is how much the model knows about a specific dataset, whereas *generalization* refers to how much the model knows about the process that generated that data.
- The mutual information of two random variables $I(X,Y) = H(X) - H(X|Y)$ represents the amount of information about $X$ that is stored in $Y$. Therefore, we can define the amount of memory stored in a trained model $\hat{\Theta}$ as $mem(X, \hat{\Theta}) = H(X) - H(X | \hat{\Theta})$ . Since this captures *all* of the information about $X$ stored in $\hat{\Theta}$, we need some way to account for generalization. Unintended memorization is the information that $\Theta$, the model prior, contains about X. Therefore, we define it as $mem_U(X, \Theta, \hat{\Theta}) = H(X, \Theta) - H(X | (\Theta, \hat{\Theta}))$ . The generalization is then defined as $mem(X, \hat{\Theta}) - mem_U(X, \Theta, \hat{\Theta})$.
- When the dataset is synthetic bitstrings, the models reach double descent exactly when the model parameters reaches the dataset size, i.e., simply memorizing the data is not longer beneficial, and the model switches to generalization.

