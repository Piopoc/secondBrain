---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, generation]
---

# Autoregressive Generation

A process of generating a sequence where each newly generated element is fed back into the model as input for the next step.

## Process in LMs
1. Start with a special token `<s>`.
2. Predict the probability distribution for the next word.
3. Sample a word $w_1$ from the distribution.
4. Use `<s>, w_1` as input to predict $w_2$.
5. Repeat until `</s>` is sampled.

## Applications
Essential for tasks like Machine Translation, Text Summarization, and Dialogue Systems.
