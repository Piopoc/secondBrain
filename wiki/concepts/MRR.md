---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# MRR

**Mean Reciprocal Rank** measures how quickly the first relevant document is found.

## Definition
The reciprocal of the rank of the first relevant document.
$$\text{RR} = \frac{1}{\text{rank of 1st relevant doc}}$$
$$\text{MRR} = \frac{1}{|Q|} \sum_{i=1}^{|Q|} \text{RR}_i$$

## Use Case
Ideal for "Known-Item Search" or Question Answering, where only one correct answer is expected.
