---
date: 2026-05-16
source: [[raw/12/]]
tags: [ir, smoothing, probability]
---

# Laplace Smoothing

Also known as additive smoothing, it is a technique used to handle the "zero-frequency problem" in probabilistic models.

## Mechanism
It adds a small positive constant $\delta$ (usually $\delta = 1$) to the count of every term in the vocabulary, ensuring that no probability is ever exactly zero.

## Formula
$$P(w_i | \Theta_d) = \frac{f_{w_i, d} + \delta}{|d| + \delta |V|}$$
Where:
- $f_{w_i, d}$ is the frequency of term $w_i$ in document $d$.
- $|d|$ is the document length.
- $|V|$ is the size of the vocabulary.
- $\delta$ is the smoothing parameter.

## Usage
Primarily used in [[Language-Models-IR]] to prevent a single missing term from making the entire query likelihood zero.
