---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, architecture]
---

# Residual Connection

Also known as "skip connections", these are connections that bypass one or more layers in a neural network.

## Purpose
In deep networks like [[Transformers]], gradients can vanish as they propagate backward. Residual connections allow the gradient to flow directly through the network, enabling the training of much deeper architectures.

## Formula
Instead of $y = f(x)$, the layer computes $y = f(x) + x$.
