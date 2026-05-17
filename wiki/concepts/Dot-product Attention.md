---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, mathematics]
---

# Dot-product Attention

The simplest form of the [[Attention Mechanism]] used to calculate the relevance of encoder states.

## Mechanism
The score is computed as the dot product between the current decoder hidden state $h^d$ and an encoder hidden state $h^e$:
$$\text{score}(h^d, h^e) = h^d \cdot h^e$$
This implements relevance as a measure of cosine similarity.
