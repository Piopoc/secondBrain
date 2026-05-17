---
date: 2026-05-16
source: [[raw/12/]]
tags: [machine-learning, optimization]
---

# Stochastic Gradient Descent

An iterative method for optimizing an objective function with suitable smoothness properties.

## Mechanism
Updates weights $w$ by taking a step in the opposite direction of the gradient of the loss function:
$$w_{t+1} = w_t - \eta \nabla L(w_t)$$

## Usage
Used to minimize [[Cross-entropy Loss]] in [[Logistic Regression]] and neural networks.
