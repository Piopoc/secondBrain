# Alternative Approaches to RAG

## Overview
Retrieval-Augmented Generation (RAG) integrates the generative power of Large Language Models (LLMs) with the factual grounding of external search systems. This summary explores the evolution from naive implementations to modular architectures.

## The RAG Paradigm Evolution

### 1. Naive RAG
The basic flow: **User Query $\rightarrow$ Retrieval $\rightarrow$ Prompt (Query + Context) $\rightarrow$ LLM $\rightarrow$ Output**.
- **Limitation:** Simple retrieval may fetch irrelevant documents or miss critical context.

### 2. Advanced RAG
Introduces pre-retrieval and post-retrieval optimizations:
- **Pre-Retrieval:** Query transformation, expansion, and optimization to improve retrieval precision.
- **Post-Retrieval:** Reranking of documents and context compression (summarization) to ensure the LLM receives only the most relevant information.

### 3. Modular RAG
A flexible architecture where components can be swapped or added:
- **Routing:** Directing the query to different retrieval sources.
- **Rewrite:** Iteratively refining the query.
- **Fusion:** Combining results from multiple retrieval strategies.
- **Memory:** Storing previous interactions to maintain context.

## Key Techniques for Improvement
- **Chunk Optimization:** Improving how documents are split (e.g., recursive retrieval).
- **Query Transformation:** Using LLMs to rewrite queries for better matching.
- **Evaluation Frameworks:** Using metrics like **Answer Relevance**, **Context Relevance**, and **Answer Faithfulness** (e.g., via tools like RAGAS or TruLens).

## Theoretical Foundations
- **Parametric Memory:** Knowledge stored within the LLM's weights during pre-training.
- **Non-Parametric Memory:** Knowledge stored in an external dense vector index (e.g., Wikipedia), accessed via a neural retriever.
- **Notable Models:**
    - **REALM:** Integrates a retriever into the pre-training phase of the language model.
    - **Web-GPT:** Uses a web-browsing environment to iteratively find references and generate answers.
