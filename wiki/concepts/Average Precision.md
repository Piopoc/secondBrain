---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# Average Precision

A metric that considers the rank of all relevant documents.

## Definition
The average of the precision values calculated at each rank where a relevant document is found.
$$\text{AP} = \frac{1}{\text{RB}} \sum_{k \in \text{Rel}} P(k)$$

## Interpretation
AP rewards systems that place relevant documents higher in the ranking.
