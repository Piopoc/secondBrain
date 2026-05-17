---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, embeddings]
---

# Positional Embedding

A method used in [[Transformers]] to provide the model with information about the order of tokens in a sequence.

## Necessity
Because [[Self-Attention]] is permutation-invariant (it treats the input as a bag of words), it has no inherent sense of sequence. Positional embeddings are added to the token embeddings to restore this information.

## Types
- **Absolute**: A unique vector for each position (1, 2, 3...).
- **Relative**: Encodes the distance between tokens.
