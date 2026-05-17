---
date: 2026-05-16
source: [[raw/12/]]
tags: [concepts, neural-ir, retrieval]
---

# Poly-encoders

**Poly-encoders** are a middle-ground architecture between Bi-encoders and Cross-encoders, designed to balance efficiency and effectiveness.

## Mechanism
Instead of a single vector for the query, a Poly-encoder produces multiple "code vectors". These vectors are then compared with the document embedding using a lightweight attention mechanism.

## Advantage
They provide a significant performance boost over Bi-encoders while remaining much faster than Cross-encoders, making them suitable for large-scale retrieval.
