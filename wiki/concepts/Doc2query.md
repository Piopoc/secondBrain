---
date: 2026-05-16
source: [[raw/12/]]
tags: [concepts, neural-ir, retrieval]
---

# Doc2query

**Doc2query** is a technique used to improve the retrieval performance of sparse models (like BM25) by augmenting documents with synthetic queries.

## Mechanism
A generative model (like T5) is used to predict potential queries that a user might ask to find a given document. These synthetic queries are then appended to the original document text.

## Advantage
It helps resolve the vocabulary mismatch problem by adding terms that are likely to appear in user queries but might be missing from the original document.
