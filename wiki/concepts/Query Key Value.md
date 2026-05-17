---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, attention]
---

# Query Key Value

The QKV framework is the mathematical core of the [[Self-Attention]] mechanism. It assigns three different roles to each input token.

## The Roles
1. **Query ($q$)**: The "search term". It represents the current token looking for relevant information from other tokens.
2. **Key ($k$)**: The "index". It represents what information the token contains, used to match against queries.
3. **Value ($v$)**: The "content". The actual information that is extracted once a match between $q$ and $k$ is found.

## Computation
The attention score is computed as:
$$\text{score}(q, k) = \frac{q \cdot k}{\sqrt{d_k}}$$
The final output for a token is a weighted sum of values $v$, where weights are determined by the softmax of the scores.
