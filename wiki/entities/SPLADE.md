# SPLADE

**SPLADE** (Sparse Lexical and Expansion) is a neural IR model that learns **sparse representations** of documents.

## Core Mechanism: Importance Estimation
Instead of a dense vector, SPLADE uses an MLM-head to map token embeddings back to a probability distribution over the entire vocabulary.
- It identifies which terms in the vocabulary are most "important" for a document, even if they don't appear literally (expansion).

## Advantages
- Combines the efficiency of inverted indices (sparse) with the semantic power of neural models (dense).
- Avoids the "black box" nature of dense retrieval by remaining in the term space.

See also: [[Bi-encoder]], [[BERT]]
