---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, architecture]
---

# Bidirectional Encoder

A model that processes the entire input sequence simultaneously, allowing each token to attend to every other token in the sequence.

## Contrast with Causal Models
While causal models (decoders) are restricted to looking at the past to predict the future, bidirectional encoders look at the "full context" to create a representation of each token.
