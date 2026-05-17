---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, architecture]
---

# Encoder-only Transformer

A Transformer architecture that consists only of the encoder blocks, lacking the causal masking found in decoders.

## Characteristics
- **Bidirectionality**: The self-attention mechanism can look at both preceding and following tokens in a sequence.
- **Purpose**: Primarily used for tasks that require a deep understanding of the input text, such as sentiment analysis, named entity recognition, and natural language inference.
- **Example**: BERT (Bidirectional Encoder Representations from Transformers).
