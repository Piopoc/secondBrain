---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# MAP

**Mean Average Precision** is the global average of Average Precision across all queries in a test set.

## Formula
$$\text{MAP} = \frac{1}{|Q|} \sum_{q \in Q} \text{AP}(q)$$

## Usage
It is the gold standard for evaluating the overall effectiveness of a ranking system.
