# Word2Vec

**Word2Vec** is a framework for learning static word embeddings using a self-supervised approach.

## Intuition
Instead of simply counting how often words co-occur, Word2Vec trains a classifier on a binary prediction task: *"Is word $C$ likely to show up near target word $w$?"*. 

## Key Mechanism
- The model does not actually care about the prediction accuracy.
- The **weights of the learned classifier** are extracted and used as the word embeddings.

## Characteristics
- Produces **Static Embeddings**.
- Captures linear analogical relations (e.g., $\text{king} - \text{man} + \text{woman} \approx \text{queen}$).

See also: [[Word Embedding]], [[Distributional Hypothesis]]
