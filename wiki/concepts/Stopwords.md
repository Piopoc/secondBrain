# Stopwords

**Stopwords** are high-frequency words in a language that carry very little semantic value for retrieval (e.g., "the", "is", "at", "which").

## Role in IR
The removal of stopwords is a common preprocessing step in the [[Lucene-Analyzer]] pipeline.

## Trade-offs
- **Advantages**:
	- **Index Size**: Drastically reduces the number of unique terms in the inverted index.
	- **Performance**: Reduces the memory footprint and speeds up the matching process.
- **Risks**:
	- **Semantic Loss**: Removing stopwords can destroy the meaning of certain phrases (e.g., "To be or not to be" becomes an empty query).

See also: [[Tokenization]], [[Lucene-Analyzer]]
