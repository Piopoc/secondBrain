---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, optimization]
---

# Vanishing Gradient Problem

A phenomenon that occurs during the training of deep neural networks, particularly [[Recurrent Neural Networks]], where the gradients of the loss function approach zero as they are propagated back through the layers.

## Impact
It prevents the weights of the early layers from updating effectively, making it nearly impossible for the network to learn long-range dependencies in a sequence.
