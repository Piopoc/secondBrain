---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, decoding]
---

# Beam Search

A heuristic search algorithm used during the decoding phase of a language model to find a more optimal sequence of tokens.

## Contrast with Greedy Decoding
Greedy decoding only picks the single best token at each step, which can lead to suboptimal global sequences. Beam Search keeps track of the $B$ most likely sequences (the "beam width") at each time step.

## Process
1. At step $t$, expand all $B$ current sequences by all possible next tokens.
2. Calculate the cumulative probability for all new candidates.
3. Keep only the top $B$ candidates and discard the rest.
4. Repeat until the end-of-sentence token is reached.
