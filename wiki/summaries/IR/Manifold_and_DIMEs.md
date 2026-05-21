# Manifold Hypothesis and DIMEs

## The Manifold Hypothesis
The **Manifold Hypothesis** suggests that real-world high-dimensional data (like document or query embeddings) actually concentrate around manifolds of much lower dimensionality.

### Application to Search
If data lies on a low-dimensional manifold, search can be simplified by looking for **linear subspaces** that best represent the association between queries and their relevant documents. This reduces noise and computational complexity.

## DIMEs (Dimension Importance Estimators)
**DIMEs** are used to quantify the importance of specific dimensions in a query representation vector $u_q \in \mathbb{R}^d$.

### How DIMEs Work
A DIME output is a query-dependent vector where each element $i$ estimates how "useful" that dimension is for producing a good ranking. Dimensions with low importance can be **zeroed out** in the query without modifying the index.

### Types of DIMEs
1. **Magnitude DIME:** Uses the absolute value of the dimension in the query itself as a proxy for importance.
2. **Active Feedback DIME:** Uses a known relevant document to simulate explicit feedback and identify important dimensions.
3. **Pseudo-Relevance Feedback DIME:** Uses the centroid of the top $\tau$ retrieved documents as a pseudo-relevant document to estimate importance.
4. **LLM DIME:** Employs an LLM to generate a response to the query, which then acts as a pseudo-relevant document.
5. **LLM-as-a-Judge DIME:** Scans the top $\tau$ retrieved documents using an LLM to judge which dimensions are most effective.
