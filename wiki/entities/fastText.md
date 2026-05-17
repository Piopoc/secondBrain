# fastText

**fastText** is an extension of the Word2Vec model that treats each word as a bag of character n-grams.

## Core Innovation: Sub-word Models
Instead of representing a word as a single atomic unit, fastText represents it as the **sum of the embeddings of its constituent n-grams**.
- Example: For $n=3$, the word "where" is represented by `<wh`, `whe`, `her`, `ere`, `re>`.

## Advantages
- **Out-of-Vocabulary (OOV) Words**: Can generate embeddings for words not seen during training by summing their n-grams.
- **Morphologically Rich Languages**: Better handles word sparsity by capturing shared roots and suffixes.

See also: [[Word Embedding]], [[Word2Vec]]
