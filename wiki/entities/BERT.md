# BERT (Bidirectional Encoder Representations from Transformers)

**BERT** is a Transformer-based model designed to produce high-quality contextualized word embeddings.

## Training Objectives
1. **Masked Language Modeling (MLM)**: Predicts "masked" tokens using the surrounding bidirectional context.
2. **Next Sentence Prediction (NSP)**: Predicts whether two sentences are adjacent in the original corpus.

## Contextual Embeddings
BERT produces a vector $Z_i$ for each token that depends on the entire sentence. Common practice is to use the final layer or the average of the last four layers.

## Common Tasks
- **Classification**: Single-input (Sentiment) or Two-input (Paraphrase).
- **Token Labeling**: NER, POS tagging, or Question Answering (span detection).

See also: [[Transformer]], [[Word Embedding]]
