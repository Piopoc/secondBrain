---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# RBP

**Rank-Biased Precision** models the user's behavior as a process of scrolling through results with a certain persistence $p$.

## Formula
$$\text{RBP} = (1-p) \sum_{m=1}^N p^{m-1} r_m$$
Where $p$ is the probability that the user continues to the next document.

## Interpretation
- $p \approx 1$: The user is patient and looks at many results.
- $p \approx 0$: The user is impatient and only looks at the first few results.
