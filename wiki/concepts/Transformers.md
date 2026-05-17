---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, architecture]
---

# Transformers

A neural network architecture that relies entirely on attention mechanisms, dispensing with recurrence.

## Key Innovations
- **[[Self-Attention]]**: Allows the model to relate different positions of a single sequence to compute a representation of the sequence.
- **Parallelization**: Since there is no recurrence, the entire sequence can be processed simultaneously.
- **Long-range Dependencies**: Better at capturing relationships between distant tokens compared to RNNs.
