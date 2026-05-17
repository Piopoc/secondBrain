---
date: 2026-05-16
source: [[raw/12/]]
tags: [entities, models, nlp]
---

# RoBERTa

**RoBERTa (Robustly Optimized BERT Pretraining Approach)** is an optimized version of BERT.

## Improvements over BERT
- **Training Data**: Trained on a much larger corpus of text.
- **Training Time**: Trained for longer.
- **Hyperparameters**: Optimized batch sizes and learning rates.
- **Dynamic Masking**: Instead of static masking during preprocessing, RoBERTa changes the mask pattern in every epoch.
- **Removal of NSP**: Found that the Next Sentence Prediction task was not necessary for improving downstream performance.
