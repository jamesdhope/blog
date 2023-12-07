---
title:  "Beyond declarative flows in virtual assistants with language models for single-Turn and multi-turn Reasoning"
categories: 
    - generativeAI
    - conversationalAI
tags: 
    - llms
    - generativeAI
    - architecture
    - watsonx
---

Building user journeys as declarative trees within a virtual assistant requires assumptions to be made about the user query and the optimal path. This is excessbated if there are many decision points and tree consists of many forks as assumptions about the path increase exponentially as the journey progresses further down the tree. To address this inefficiency of design, one approach is to use a language model to reason over available tools (or APIs) that might be used to respond to the query. This approach collapses decision points in the tree and replaces it with a language model. Additionally, the language model can be guided through a policy or rules expressed in natural language and supplied to the model in a prompt.

The following diagram shows this interaction with IBM Watson Assistant which is used to orchestrate the call to the language model for reasoning, the tools, and the language model again to generate a final response.

![Interaction Diagram](/assets/images/single-turn-reasoning.png)

In this example, the language model is used for single turn reasoning. With next generation, stateful language models, multi-turn reasoning may be more effective at guiding the user to a goal.