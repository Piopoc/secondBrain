---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, generation]
---

# Decoding Strategies

The methods used by a Large Language Model to select the next token from the probability distribution produced by the final softmax layer.

## Deterministic Methods
- **Greedy Decoding**: Always selects the token with the highest probability. Fast but can lead to repetitive or suboptimal text.

## Stochastic Methods
- **Random Sampling**: Samples from the full distribution. High diversity but can be incoherent.
- **Top-k Sampling**: Samples only from the $k$ most likely tokens.
- **Top-p (Nucleus) Sampling**: Samples from the smallest set of tokens whose cumulative probability exceeds $p$.
- **Temperature Sampling**: Reshapes the distribution. 
    - **Low Temp**: Makes the distribution "sharper" (more deterministic).
    - **High Temp**: Makes the distribution "flatter" (more diverse).
