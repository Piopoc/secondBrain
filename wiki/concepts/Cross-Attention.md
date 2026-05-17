---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, attention]
---

# Cross-Attention

A specific type of attention used in [[Encoder-Decoder Transformer]]s to link the encoder and decoder.

## Mechanism
In a standard self-attention layer, Q, K, and V all come from the same source. In **Cross-Attention**:
- **Query (Q)**: Comes from the previous layer of the **Decoder**.
- **Key (K)** and **Value (V)**: Come from the final output of the **Encoder**.

This allows the decoder to "look back" at the original source sequence to decide which parts are most relevant for the current token being generated.
