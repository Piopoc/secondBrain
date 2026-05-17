---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# Precision

A metric that measures the accuracy of the retrieved set.

## Definition
The proportion of retrieved documents that are actually relevant.
$$\text{Precision} = \frac{|A \cap B|}{|B|}$$
Where:
- $A$ is the set of all relevant documents.
- $B$ is the set of all retrieved documents.

## Interpretation
High precision means the system returns very few irrelevant documents ("noise").
