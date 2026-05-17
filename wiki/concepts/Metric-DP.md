---
date: 2026-05-16
source: [[raw/12/]]
tags: [privacy, embeddings, neural-ir]
---

# Metric-DP

An adaptation of [[Differential Privacy]] specifically designed for high-dimensional vector spaces, such as those used for word or document embeddings.

## Motivation
Traditional DP adds noise to scalar counts or sums. In IR, we deal with embeddings. Metric-DP adds noise directly to the embedding vectors in the vector space.

## Goal
To protect the "semantic nuance" of a query while ensuring that the resulting offuscated vector cannot be used to uniquely identify the original input.
