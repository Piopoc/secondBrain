# Vector Space Model (VSM)

The **Vector Space Model (VSM)** represents documents and queries as vectors in a high-dimensional space, where each dimension corresponds to a unique term in the vocabulary.

## Core Mechanism
Relevance is measured by the distance or angle between the query vector $\vec{q}$ and the document vector $\vec{d}$. The most common measure is [[Cosine-Similarity]].

## Term Weighting
To handle the fact that not all terms are equally important, VSM typically uses the [[TF-IDF]] weighting scheme.

## Advantages
- **Ranking**: Unlike the [[Boolean-Model]], VSM provides a ranked list of documents.
- **Partial Match**: Documents that share some terms with the query are still retrieved.

See also: [[Cosine-Similarity]], [[TF-IDF]], [[Information-Retrieval]]
