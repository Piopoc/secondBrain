# Language Models for IR

**Language Models (LM)** for IR treat each document as a probability distribution over a vocabulary.

## Core Idea
Instead of calculating a similarity score, the system asks: *"What is the probability that this document model generated the query?"*

## Unigram Model
The simplest LM assumes that words are generated independently (Unigrams). The probability of a document $D$ given a query $Q$ is the product of the probabilities of each word in $Q$ appearing in $D$.

## The Zero-Probability Problem
If a query word is missing from a document, the probability becomes $0$. To solve this, **Smoothing** techniques are used:
- [[Jelinek-Mercer-Smoothing]]: A linear interpolation between the document model and the collection model.
- [[Dirichlet-Smoothing]]: A Bayesian approach that adds virtual words to the document.

See also: [[Information-Retrieval]]
