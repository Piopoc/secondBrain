---
date: 2026-05-16
source: [[raw/12/]]
tags: [machine-learning, classification]
---

# Logistic Regression

A linear model used for binary classification that predicts the probability of a target variable.

## Binary Logistic Regression
Uses the [[Sigmoid Function]] to map a linear combination of features to a value between 0 and 1.
- **Formula**: $P(+) = \sigma(wx) = \frac{1}{1 + \exp(-wx)}$
- **Logit**: The inverse of the sigmoid, $\text{logit}(p) = \ln \frac{p}{1-p}$.

## Optimization
- **Loss Function**: [[Cross-entropy Loss]].
- **Algorithm**: [[Stochastic Gradient Descent]].
