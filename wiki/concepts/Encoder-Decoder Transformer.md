---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, architecture]
---

# Encoder-Decoder Transformer

A Transformer architecture that combines a bidirectional encoder and a causal decoder, specifically designed for sequence-to-sequence (seq2seq) tasks.

## Workflow
1. **Encoder**: Processes the source sequence into a set of contextualized representations $H^{enc}$.
2. **Decoder**: Generates the target sequence token by token. At each step, it attends to:
    - The previously generated tokens (via self-attention).
    - The encoder's output (via [[Cross-Attention]]).

## Primary Use Case
Machine Translation, where the encoder processes the source language and the decoder generates the target language.
