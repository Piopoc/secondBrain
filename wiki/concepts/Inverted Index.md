---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, indexing, data-structure]
---

# Inverted Index

The fundamental data structure used by almost all modern search engines to enable efficient full-text search.

## Concept
Instead of mapping a document to the terms it contains (forward index), an inverted index maps each unique term in the corpus to a list of documents (postings list) that contain that term.

## Structure
- **Dictionary**: A sorted list of all unique terms in the corpus.
- **Postings List**: For each term, a list of document IDs where the term appears, often including the frequency and positions of the term.

## Advantage
It allows the system to find all documents containing a specific term in $O(1)$ or $O(\log V)$ time, regardless of the total number of documents in the collection.
