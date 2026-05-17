---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, neural-networks]
---

# Neural Language Models

Neural networks designed to predict the next word in a sequence given a previous context.

## Architecture
- **Input**: A fixed context window of words (e.g., size 3).
- **Representation**: Words are initially represented via [[One-hot Encoding]] and then mapped to an [[Embedding Vector]].
- **Processing**: The embeddings are passed through [[Feedforward Neural Networks]] (hidden layers).
- **Output**: A [[Softmax Function]] over the entire vocabulary to determine the probability $P(w_t | w_{t-k}, \dots, w_{t-1})$.
