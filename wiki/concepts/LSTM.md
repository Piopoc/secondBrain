---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, sequential-data]
---

# LSTM

**Long Short-Term Memory** is a specialized type of [[Recurrent Neural Networks]] designed to overcome the [[Vanishing Gradient Problem]].

## Mechanism
LSTMs use a complex system of "gates" to manage the [[Hidden State]]:
1. **Forget Gate**: Removes information no longer needed from the context.
2. **Input/Update Gate**: Adds new information likely to be useful for future decisions.
