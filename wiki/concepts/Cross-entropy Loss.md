---
date: 2026-05-16
source: [[raw/12/]]
tags: [machine-learning, loss-function]
---

# Cross-entropy Loss

A loss function used to measure the performance of a classification model whose output is a probability value between 0 and 1.

## Formula (Binary)
$$L_{CE}(\hat{y}, y) = -(y \log \hat{y} + (1-y) \log(1-\hat{y}))$$

## Usage
Standard loss function for [[Logistic Regression]] and neural networks.
