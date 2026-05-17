# 🧠 Neural IR and Embeddings

This document explores the transition from sparse to dense representations in Information Retrieval, the architecture of Transformers, and the evolution of Neural IR models.

## 1. Word Embeddings

### Sparse vs. Dense Representations
- **Sparse Representations**: Most components are zero; terms do not appear in every query/document. Semantically close elements may end up in different vector representations.
- **Dense Representations**: All components contain real values (rarely zero). The dimension of the vector is fixed beforehand. See [[Word-Embedding]]. 

### Distributional Hypothesis
The core idea is the [[Distributional-Hypothesis]]: **words that occur in the same contexts tend to have similar meanings**. 
- A word is represented as a real-value vector called an **Embedding**.
- The standard measure for similarity between two embeddings is [[Cosine-Similarity]].

### Static Word Embeddings
Compute **global representations**: a single fixed vector for each term in the vocabulary, regardless of context.
- [[entities/Word2Vec]]: Based on a self-supervised approach. Instead of counting co-occurrences, it trains a classifier on a binary prediction task.
- [[entities/GloVe]]: Based on ratios of probabilities from the word-word co-occurrence matrix.
- [[entities/fastText]]: Extends Word2Vec by using **sub-word models** to handle **out-of-vocabulary (OOV)** words.

**Properties**:
- **Analogical Relations**: Static embeddings can capture linear relationships.
- **Limitations**: No contextualization; difficulty handling local context and ordering.

### Contextualized Word Embeddings
Compute **local representations** that depend on the surrounding tokens.
- Each token is associated with a different vector every time it appears, depending on its context.
- Examples: [[entities/BERT]], [[entities/RoBERTa]], [[entities/GPT]].

---

## 2. Transformers and BERT

### Transformer Architecture
A complex classifier based on an **Encoder-Decoder** structure and **Self-Attention**. See [[entities/Transformer]].
- **Main Innovation**: Self-attention allows for significant parallelization and better learning of long-range dependencies.
- **Encoder models**: Best suited for tasks requiring an understanding of the full sequence.
- **Decoder models**: Best suited for text generation.
- **Causal Transformers (e.g., GPT)**: Consider only previous tokens in the sequence.

### BERT (Bidirectional Encoder Representations from Transformers)
Detailed in [[entities/BERT]].
- **Mask-based Learning**: Predicts words from surrounding contexts.
- **Next Sentence Prediction (NSP)**: Predicts whether two sentences are actual adjacent pairs.
- **Contextual Embeddings**: The output vector $Z_i$ represents token $x_i$ in the context of the whole sentence.

### BERT Tasks
1. **Single-input classification**: e.g., Sentiment Analysis.
2. **Two-input classification**: e.g., Paraphrase detection, Entailment.
3. **Single-input token labeling**: e.g., [[NER]], [[POS-Tagging]].
4. **Two-input token labeling**: e.g., Question Answering.

---

## 3. Neural IR Models

The relevance score $s(q,d)$ can be generalized as:
$$s(q,d) = f(\phi(q), \psi(d), \eta(q,d))$$
Where:
- $\phi(q)$: Query representation function.
- $\psi(d)$: Document representation function.
- $\eta(q,d)$: Interaction function between query and document.
- $f$: Aggregation function.

### Interaction-focused Models ([[Cross-encoder]])
Detailed in [[Cross-encoder]].
- The interaction $\eta(q,d)$ is explicitly constructed.
- **Pros**: Substantial performance improvements.
- **Cons**: Extremely slow; often used only as a **Re-ranker**.

### Representation-focused Models ([[Bi-encoder]] / Dual-encoders)
Detailed in [[Bi-encoder]].
- $\eta(q,d)$ is not present. Query and document representations are computed independently.
- **Pros**: Extremely fast; document embeddings can be precomputed.
- **DPR (Dense Passage Retriever)**: See [[entities/DPR]].

### Advanced Neural Retrieval
- **Multiple Representations (Late Interaction)**: Uses more than one embedding per text.
- **[[Poly-encoders]]**: A middle ground between Bi-encoders and Cross-encoders.
- **[[Doc2query]] / DocT5query**: Generates potential queries for a document.
- **SPLADE**: See [[entities/SPLADE]]. Uses **Importance Estimation** to create sparse but learned representations.
