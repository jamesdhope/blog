---
title:  "Contrastive Perplexity for context suppression and reduced token count for in-context learning, RAG applications"
categories: 
    - generativeAI
    - conversationalAI
tags: 
    - llms
    - generativeAI
    - architecture
    - conversationalAI
    - watsonx
    - rag
---

Contrastive perplexity has been proposed as an approach to reduce irrelevant context in the post retrieval stage of a RAG application. Contrastive perplexity evaluates how well the model can distinguish between different embedded passages contained within the search results and the original user query. The lower the contrastive perplexity score the more relevant the passage, and passages with a higher contrastive perplexity score can be disregarded.

The pseudo-mathematical approach is as follows:

Step 1 Fetch passages, $$P$$, from the embeddings store based on the user query.

Step 2 Calculate the conditional probility of all retrieved passages given the user query as the dot product of the two embeddings as <span style="font-size: smaller;">$$ \prod_{i=1}^{N} p_{i} \cdot \text{userQuery} $$</span>.

Step 3: Calculate Perplexity (the exponential of the cross entropy) for all passage in $$P$$ as <span style="font-size: smaller;">$$2^{-\frac{1}{N}\sum_{i=1}^{N}\log_2 P(w_i|w_1, w_2, ..., w_{i-1})}$$</span> where $$N$$ is the number of words (or tokens) in the passage, or the length of the vectorised passage. Note this is equivalent to <span style="font-size: smaller;">$$\sqrt[N]{\frac{1}{P(w_1, w_2, ..., w_N)}} $$.</span>

Step 3 Compare the perplexities of different passages by calculating their quotient $$\frac{\text{passage}_{i}}{\text{passage}_{j}}$$ for all pairs $$i$$ and $$j$$. Lower contrastive perplexity indicates that the passage is more consistent with the language model's understanding of the user query.

Step 4 Disgregard passages with a higher contrastive perplexity score. These passages are more likely to be contextually relevant and coherent with the user's intent.

This approach reduces the likelihood of the 'lost in the middle problem', where the model fails to extract the most relevant context by reducing the most irrelevant context in the post retrieval stage. Furthermore, this approach supresses the context to reduce token count, reduce inferencing costs and potentially decrease overall RAG latency.

References

[1] https://blog.llamaindex.ai/longllmlingua-bye-bye-to-middle-loss-and-save-on-your-rag-costs-via-prompt-compression-54b559b9ddf7

[2] https://towardsdatascience.com/perplexity-in-language-models-87a196019a94

[3] https://arxiv.org/pdf/1405.2061.pdf