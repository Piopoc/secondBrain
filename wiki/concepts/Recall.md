---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# Recall

A metric that measures the completeness of the retrieved set.

## Definition
The proportion of all relevant documents in the corpus that were successfully retrieved.
$$\text{Recall} = \frac{|A \cap B|}{|A|}$$
Where:
- $A$ is the set of all relevant documents.
- $B$ is the set of all retrieved documents.

## Interpretation
High recall means the system finds most of the relevant information, even if it includes some noise.
