# Vocabulary Mismatch

**Vocabulary Mismatch** is the fundamental limitation of lexical (sparse) retrieval systems.

## Definition
It occurs when the user's query and the relevant documents use different words to describe the same concept.
- **Example**: User searches for "auto", but the document contains "automobile".

## Impact
In a pure term-matching system, this results in a score of $0$, meaning the relevant document is not retrieved despite being semantically perfect.

## Solutions
1. **Lexical Solutions**: Using [[Stemming]], synonyms (Thesauri), or [[N-Grams]].
2. **Semantic Solutions**: Using [[Word Embedding]] and Neural IR models (Dense Retrieval), which map different words with similar meanings to the same vector space.

See also: [[Information-Retrieval]], [[Word Embedding]]
