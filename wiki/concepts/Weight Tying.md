---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, optimization]
---

# Weight Tying

A technique where the weights of the input embedding matrix are shared with the weights of the final output linear layer.

## Benefit
It reduces the total number of parameters in the model and often improves performance by forcing the model to use the same semantic representation for both input and output.
