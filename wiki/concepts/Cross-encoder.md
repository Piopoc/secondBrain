# Cross-encoder

A **Cross-encoder** is a neural IR model where the query and document are fed into the network **simultaneously**.

## Mechanism
The interaction $\eta(q,d)$ is explicitly constructed. The model processes the pair $(q, d)$ as a single input sequence, allowing the attention mechanism to capture deep interactions between every query token and every document token.

## Pros and Cons
- **Pros**: High accuracy and substantial performance improvements.
- **Cons**: Extremely slow. The score $s(q,d)$ cannot be precomputed, making it infeasible for large-scale initial retrieval.
- **Usage**: Typically used as a **Re-ranker** for a small set of candidates.

See also: [[Bi-encoder]], [[Transformer]]
