---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, attention]
---

# Multi-Head Attention

An extension of the [[Attention Mechanism]] that allows the model to attend to information from different representation subspaces at different positions simultaneously.

## Mechanism
Instead of one large attention operation, the model uses multiple "heads". Each head has its own set of $W^q, W^k, W^v$ weights.
1. Each head computes its own attention output.
2. All head outputs are concatenated.
3. The result is projected back to the original dimension using a linear layer $W^O$.

## Advantage
This allows the model to capture diverse relationships (e.g., one head focuses on the subject of the sentence, another on the verb).
