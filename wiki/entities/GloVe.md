# GloVe (Global Vectors)

**GloVe** is a model for static word embeddings that combines the advantages of global matrix factorization and local context window methods.

## Core Mechanism
- Based on **ratios of co-occurrence probabilities** from a global word-word co-occurrence matrix.
- It is trained only on the non-zero elements of the matrix, making it more efficient than processing the entire corpus via sliding windows.

## Characteristics
- Produces **Static Embeddings**.
- Leverages global statistics of the corpus.

See also: [[Word Embedding]], [[Word2Vec]]
