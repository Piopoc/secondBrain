---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, representation]
---

# Contextual Embedding

A vector representation of a token that changes depending on the other tokens present in the sequence.

## Contrast with Static Embeddings
Unlike Word2Vec or GloVe, where the word "bank" always has the same vector, a [[Contextual Embedding]] will produce different vectors for "bank" in "river bank" vs "investment bank".

## Generation
In Transformers, these are the output vectors of the transformer blocks. A common practice is to average the embeddings from the last 4 layers to get a more stable representation.
