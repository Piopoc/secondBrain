---
date: 2026-05-16
source: [[raw/12/]]
tags: [machine-learning, classification]
---

# Multinomial Logistic Regression

An extension of [[Logistic Regression]] used for multi-class classification problems.

## Mechanism
Instead of a single sigmoid output, it uses the [[Softmax Function]] to produce a probability distribution over $K$ possible classes.
- **Weight Interpretation**: The weights $W$ for each class can be viewed as "prototypes" of that class.
