---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, optimization]
---

# Layer Normalization

A technique used to stabilize the hidden state dynamics in deep neural networks.

## Mechanism
It normalizes the activations across the feature dimension for each training example independently. This ensures that the mean and variance of the inputs to each layer remain consistent.

## Usage
Crucial in [[Transformers]] to prevent internal covariate shift and speed up convergence.
