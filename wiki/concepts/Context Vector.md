---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, representation]
---

# Context Vector

In an [[Encoder-Decoder Architecture]], the context vector is the fixed-length representation of the entire input sequence.

## The Bottleneck Problem
Because the vector has a fixed size, it must compress all information from the source text. This creates a bottleneck that limits the model's performance on long sequences, a problem solved by the [[Attention Mechanism]].
