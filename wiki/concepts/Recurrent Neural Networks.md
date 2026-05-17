---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, sequential-data]
---

# Recurrent Neural Networks

A class of neural networks designed to recognize patterns in sequences of data, such as text, genomes, or stock market data.

## Core Mechanism
Unlike Feedforward networks, RNNs have connections that form directed cycles. This allows them to maintain a [[Hidden State]] that captures information about what has been seen in previous steps of the sequence.

## Mathematical Form
The state at time $t$ is computed as:
$$h_t = g(U h_{t-1} + W x_t)$$
Where:
- $x_t$ is the input at time $t$.
- $h_{t-1}$ is the previous hidden state.
- $g$ is a non-linear [[Activation Function]] (e.g., tanh, ReLU).

## Unrolling
RNNs are often visualized as "unrolled" in time, where each time step is represented as a separate layer of the same network sharing the same weights $U$ and $W$.
