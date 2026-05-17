# N-Grams

**N-Grams** are contiguous sequences of $n$ items from a given sample of text or speech.

## Types
1. **Word N-grams**:
	- **Bigrams** ($n=2$), **Trigrams** ($n=3$).
	- Used to capture multi-word entities (e.g., "New York").
	- **Trade-off**: Significantly increases the size of the inverted index.
2. **Character N-grams**:
	- A sliding window of $n$ characters.
	- Used as a fallback for languages without available stemmers.
	- Helps in handling typos and morphological variations.

See also: [[Tokenization]], [[Stemming]]
