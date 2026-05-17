---
date: 2026-05-16
source: [[raw/12/]]
tags: [privacy, data-protection, anonymity]
---

# K-Anonymity

A property of a dataset used to protect the privacy of individuals by ensuring they cannot be uniquely identified.

## Definition
A dataset satisfies **k-anonymity** if every record in the dataset is indistinguishable from at least $k-1$ other records with respect to a set of **quasi-identifiers** (e.g., age, zip code, gender).

## Mechanism
Achieved through:
- **Generalization**: Replacing a specific value with a more general one (e.g., "Age 24" $\rightarrow$ "Age 20-30").
- **Suppression**: Removing a value entirely if it cannot be generalized enough to meet the $k$ threshold.

## Limitation
k-anonymity is vulnerable to **homogeneity attacks** (if all $k$ records have the same sensitive attribute) and **background knowledge attacks**.
