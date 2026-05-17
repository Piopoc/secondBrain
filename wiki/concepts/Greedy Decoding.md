---
date: 2026-05-16
source: [[raw/12/]]
tags: [nlp, decoding]
---

# Greedy Decoding

The simplest form of decoding in sequence generation tasks.

## Mechanism
At each time step $t$, the model selects the token with the highest probability from the softmax output:
$$w_t = \text{argmax}_w P(w | w_{<t})$$

## Limitations
- **Local Optima**: It makes the best local choice at each step, which may not lead to the best overall sequence.
- **Lack of Diversity**: Produces deterministic and often repetitive text.
- **No Backtracking**: Once a token is chosen, it cannot be changed, even if it leads to a very low probability for the rest of the sentence.

## Alternative
[[Beam Search]] is used to mitigate these issues by exploring multiple paths.
