---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, training]
---

# Next Sentence Prediction

A binary classification task used to train models to understand the relationship between two sentences.

## Process
The model is given two sentences (A and B) and must predict whether B actually follows A in the original text.
- **Input**: `[CLS] Sentence A [SEP] Sentence B [SEP]`
- **Utility**: Helps the model capture discourse-level coherence and semantic relationships between sentences.
