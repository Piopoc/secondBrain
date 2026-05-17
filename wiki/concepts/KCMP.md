---
date: 2026-05-16
source: [[raw/12/]]
tags: [privacy, obfuscation, ir]
---

# KCMP

**Calibrated Multivariate Perturbations (KCMP)** is a method for query obfuscation that protects user privacy while maintaining retrieval utility.

## Workflow
1. **Preprocessing**: Tokenization and conversion of the query into embeddings.
2. **Perturbation**: Calculating a noise vector based on a probability density function for each word.
3. **Selection**: Choosing a replacement word whose embedding best approximates the perturbed vector.

## Limitations
- It ignores the global distribution of embeddings (can be improved with Mahalanobis distance).
- It may occasionally replace a word with itself.
- It treats words independently, ignoring the sequential context.
