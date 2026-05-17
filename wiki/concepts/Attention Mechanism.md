---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, mechanism]
---

# Attention Mechanism

A technique that allows a model to focus on specific parts of the input sequence when producing an output.

## Function
Instead of relying on a single static [[Context Vector]], the decoder computes a dynamic context vector for each output step. This is done by taking a weighted sum of all encoder hidden states.

## Computation
1. **Score**: Compute similarity between decoder state and encoder states (e.g., [[Dot-product Attention]]).
2. **Weights**: Normalize scores using [[Softmax Function]].
3. **Sum**: Compute the weighted sum of encoder states.
