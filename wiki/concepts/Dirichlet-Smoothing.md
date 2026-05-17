# Dirichlet Smoothing

**Dirichlet Smoothing** is a Bayesian approach to smoothing in Language Models for IR.

## Mechanism
Instead of a simple linear interpolation, it assumes that the document is a sample from a Dirichlet distribution. In practice, this means adding a fixed amount of "virtual" word counts (based on the collection distribution) to the document's counts.

## Comparison with Jelinek-Mercer
While Jelinek-Mercer uses a constant $\lambda$, Dirichlet smoothing effectively adjusts the weight of the collection model based on the length of the document (shorter documents get more smoothing).

See also: [[Language-Models-IR]], [[Jelinek-Mercer-Smoothing]]
