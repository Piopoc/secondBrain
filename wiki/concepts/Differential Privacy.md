---
date: 2026-05-16
source: [[raw/12/]]
tags: [privacy, mathematics, noise]
---

# Differential Privacy

A rigorous mathematical definition of privacy that ensures the output of an algorithm does not reveal whether a specific individual's data was used in the computation.

## Definition ($\epsilon$-DP)
An algorithm $M$ is $\epsilon$-differentially private if for any two neighboring datasets $D_1$ and $D_2$ (differing by only one record), the probability of any output $S$ is nearly the same:
$$P(M(D_1) \in S) \le e^\epsilon \cdot P(M(D_2) \in S)$$

## The Privacy Budget ($\epsilon$)
- **Small $\epsilon$**: High privacy, more noise added, lower utility.
- **Large $\epsilon$**: Low privacy, less noise, higher utility.

## Mechanism
Typically implemented by adding calibrated noise (e.g., Gaussian or Laplace noise) to the result of a query.
