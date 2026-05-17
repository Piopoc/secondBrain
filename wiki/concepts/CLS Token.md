---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, tokens]
---

# CLS Token

A special token (Classification token) prepended to the input of an [[Encoder-only Transformer]].

## Purpose
The final hidden state corresponding to the `[CLS]` token is intended to serve as a summary representation of the entire input sequence. This vector is typically used as the input to a classifier head for tasks like sentiment analysis or [[Next Sentence Prediction]].
