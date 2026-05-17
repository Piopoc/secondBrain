# Bi-encoder

A **Bi-encoder** (or Dual-encoder) is a neural IR model where the query and document are encoded **independently**.

## Mechanism
The query $\phi(q)$ and document $\psi(d)$ are mapped into the same vector space. The relevance score is typically computed as a simple dot product or cosine similarity:
$$s(q,d) = \phi(q) \cdot \psi(d)$$

## Pros and Cons
- **Pros**: Extremely fast. Document embeddings can be precomputed and stored in a vector index (e.g., FAISS).
- **Cons**: Lower accuracy than Cross-encoders because it ignores the explicit interaction between query and document tokens.

See also: [[Cross-encoder]], [[DPR]]
