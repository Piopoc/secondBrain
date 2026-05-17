# Word Embedding

A **Word Embedding** is a dense, real-valued vector representation of a word in a continuous vector space.

## Core Characteristics
- **Dense Representation**: Unlike sparse vectors (where most components are zero), embeddings contain real values in all dimensions.
- **Fixed Dimensionality**: The size of the vector is predetermined (e.g., 100, 300 dimensions).
- **Semantic Proximity**: Words with similar meanings are mapped to points close to each other in the vector space.

## Measurement
The standard measure for similarity between two word embeddings is **Cosine Similarity**.

## Types
- **Static Embeddings**: A word has a single fixed vector regardless of context (e.g., [[Word2Vec]], [[GloVe]], [[fastText]]).
- **Contextualized Embeddings**: The vector changes based on the surrounding tokens (e.g., [[BERT]], [[GPT]]).

See also: [[Distributional Hypothesis]]
