---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# P@K

**Precision at K** is a rank-based metric that measures precision only for the top $K$ results.

## Definition
$$\text{P@K} = \frac{\text{Relevant documents in top K}}{K}$$

## Limitation: The Recall Base (RB)
P@K is limited by the total number of relevant documents ($\text{RB}$). If $\text{RB} < K$, the maximum possible $\text{P@K}$ is $\text{RB}/K$, even for a perfect system.
