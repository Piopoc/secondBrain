---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, architecture]
---

# Feedforward Neural Networks

A type of artificial neural network where connections between the nodes do not form a cycle.

## Structure
- **Input Layer**: Receives the raw features.
- **Hidden Layer(s)**: Perform non-linear transformations using [[Activation Function]]s.
- **Output Layer**: Produces the final prediction (e.g., using [[Softmax Function]] for classification).

## Neural Unit
A unit takes a set of real-valued inputs $x_i$, computes a weighted sum $z = \sum w_i x_i$, and applies a non-linear function $\sigma(z)$ to produce the output $a$.
