---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# R-Precision

A metric that evaluates precision at a specific rank equal to the number of relevant documents.

## Definition
Precision calculated at $K = \text{Recall Base (RB)}$.
$$\text{R-prec} = \text{P@RB}$$

## Advantage
It provides a fair comparison between queries with different numbers of relevant documents, as it evaluates each system at its theoretical maximum recall.
