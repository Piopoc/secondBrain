---
date: 2026-05-16
source: [[raw/12/]]
tags: [transformers, models]
---

# T5 Model

**T5 (Text-to-Text Transfer Transformer)** is a unified framework that treats every NLP task as a text-to-text problem.

## Architecture
It uses a standard [[Encoder-Decoder Transformer]] architecture.

## The Text-to-Text Paradigm
Instead of having different heads for different tasks (e.g., a classification head for sentiment), T5 uses a natural language prompt to specify the task:
- **Translation**: "translate English to German: The cat is on the mat" $\rightarrow$ "Die Katze ist auf der Matte"
- **Summarization**: "summarize: [text]" $\rightarrow$ "[summary]"
- **Classification**: "sentiment: This movie is great" $\rightarrow$ "positive"
