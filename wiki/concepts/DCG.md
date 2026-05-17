---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# DCG

**Discounted Cumulative Gain** is a metric used for multi-graded relevance (e.g., 0=Irrelevant, 1=Slightly, 2=Relevant, 3=Perfect).

## Formula
$$\text{DCG}(K) = \sum_{i=1}^K \frac{r_i}{\log_2(i+1)}$$
Where $r_i$ is the relevance grade of the document at position $i$.

## Logic
It rewards the system for placing highly relevant documents at the top of the list, while "discounting" the value of relevant documents found lower down.
