---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, training]
---

# Teacher Forcing

A training strategy for recurrent neural networks where the ground-truth output from the training dataset is used as the input for the next time step, rather than the model's own predicted output.

## Purpose
It prevents "error accumulation" during training, where a single wrong prediction at the start of a sequence would lead the model to diverge further and further from the correct path.
