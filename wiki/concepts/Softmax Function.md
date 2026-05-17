---
date: 2026-05-16
source: [[raw/12/]]
tags: [mathematics, activation-function]
---

# Softmax Function

A function that turns a vector of $K$ real values into a probability distribution consisting of $K$ probabilities proportional to the exponentials of the input numbers.

## Formula
$$\text{softmax}(y_i) = \frac{\exp y_i}{\sum_{j=1}^K \exp y_j}$$

## Usage
Used in the output layer of [[Multinomial Logistic Regression]] and [[Feedforward Neural Networks]] for multi-class classification.
