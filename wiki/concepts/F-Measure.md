---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, evaluation, metric]
---

# F-Measure

A single metric that combines Precision and Recall into a single value.

## Definition
The harmonic mean of Precision ($P$) and Recall ($R$).
$$F = \frac{2 \cdot P \cdot R}{P + R}$$

## Why Harmonic Mean?
Unlike the arithmetic mean, the harmonic mean penalizes extreme values. If either Precision or Recall is very low, the F-Measure will also be low, forcing the system to balance both.
