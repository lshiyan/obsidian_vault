https://arxiv.org/pdf/2504.19413

- MAIN IDEA: Persistent memory is necessary to avoid context overflow in agents.
- LLM's are limited by fixed-context windows, cannot remember information after context overflow.
- Separated into extraction and update phases.
- Extraction phase initiates upon reception of a new message pair $<m_t,m_{t-1}>$, which typically is a new assistant user message pair. To facilitate context-aware retrieval, they include an asynchronously generated summary of the entire conversation $S$, and a sequence of recent messages $<m_{t-h}...m_{t-2}>$, where $h$ is a hyperparameter specifying the temporal locality. The combination of all these forms a prompt with which an LLM extracts relevant historical data.
- In the update phase, each extracted fact $\omega_i$ is evaluated against existing memories to maintain consistency. LLM's can add, update, delete, or no op each memory.
- This process can be augmented with a knowledge graph to represent memory. In the extraction phase, a entity extractor model is pair with a relations generator in order to extract relevant tuples from a new message.
- New facts are tested using a conflict detection mechanism to possibly test against redundant or conflicting data.
- Retrieval identifies nodes that are relevant to the query, and performs traversal to obtain relevant relationship triplets. The most relevant ones are then used to answer the questions.