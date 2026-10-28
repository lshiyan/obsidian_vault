https://arxiv.org/pdf/2201.02177

- MAIN IDEA: Neural networks can exhibit perfect generalization past the point of overfitting on training data, with no real changes to held out data.![[Pasted image 20260730131714.png]]
- The training data is binary operations of the form $a \circ b$ , where $\circ$ is any binary operation. For the inputs, the networks are given abstract representations of the elements.
- More pronounced on small datasets, larger datasets show training and validation curves that track more closely.
- The model they used is a decoder only transformer with causal attention masking.
- Show that weight decay can have a large effect on efficiency of convergence, as well as Gaussian noise.