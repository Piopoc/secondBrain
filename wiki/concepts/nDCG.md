---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# nDCG

**Normalized Discounted Cumulative Gain** is the normalized version of DCG.

## Formula
$$\text{nDCG} = \frac{\text{DCG}}{\text{iDCG}}$$
Where $\text{iDCG}$ is the Ideal DCG (the score obtained if all relevant documents were sorted perfectly).

## Advantage
Allows comparing the performance of a system across different queries, regardless of the number of relevant documents available for each.
