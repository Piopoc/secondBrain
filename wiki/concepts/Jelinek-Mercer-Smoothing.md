# Jelinek-Mercer Smoothing

**Jelinek-Mercer Smoothing** is a technique used in Language Models for IR to avoid zero probabilities for terms not present in a document.

## Mechanism
It computes the final probability of a term as a weighted linear combination of the term's probability in the document and its probability in the entire collection:
$$P(w | D) = (1-\lambda) P_{MLE}(w | D) + \lambda P_{MLE}(w | C)$$

## Interpretation
- $\lambda = 0$: Pure document model (high variance).
- $\lambda = 1$: Pure collection model (ignores the document).
- $0 < \lambda < 1$: A balance that ensures every term in the vocabulary has a non-zero probability.

See also: [[Language-Models-IR]], [[Dirichlet-Smoothing]]
