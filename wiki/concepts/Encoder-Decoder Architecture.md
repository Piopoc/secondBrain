---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, architecture]
---

# Encoder-Decoder Architecture

A neural network design used primarily for sequence-to-sequence tasks (e.g., Machine Translation).

## Components
1. **Encoder**: Processes the input sequence and generates a sequence of contextualized representations.
2. **Context Vector**: The final state of the encoder that captures the "essence" of the input.
3. **Decoder**: Uses the context vector to generate an output sequence of arbitrary length.
