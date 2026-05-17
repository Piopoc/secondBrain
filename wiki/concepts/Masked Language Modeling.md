---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, training]
---

# Masked Language Modeling

A self-supervised training objective used to train [[Encoder-only Transformer]]s.

## Mechanism
1. A random sample of tokens is selected from the input.
2. These tokens are either:
    - Replaced with a `[[CLS Token]]` (specifically the `[MASK]` token).
    - Replaced with a random token from the vocabulary.
    - Left unchanged.
3. The model is trained to predict the original token for these positions using the surrounding context.
