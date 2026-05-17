---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, embeddings]
---

# Segment Embedding

An additional embedding added to the token and positional embeddings to distinguish between different segments of the input.

## Purpose
When a model is given two sentences (A and B), segment embeddings (e.g., a vector of 0s for sentence A and 1s for sentence B) allow the model to easily identify which token belongs to which sentence.
