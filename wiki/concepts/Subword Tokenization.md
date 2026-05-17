---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, tokenization]
---

# Subword Tokenization

A tokenization strategy that breaks words into smaller, frequent units (subwords) rather than whole words or individual characters.

## Motivation
- **Vocabulary Size**: Prevents the vocabulary from becoming too large (as with word-level tokenization).
- **OOV Problem**: Handles Out-of-Vocabulary words by breaking them into known sub-components.

## Components
Typically involves a **Token Learner** (to build the vocabulary) and a **Token Segmenter** (to split the text).
