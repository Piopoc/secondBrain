# Zipf's Law

**Zipf's Law** is an empirical law stating that in a corpus of natural language, the frequency of any word is inversely proportional to its rank in the frequency table.

## Formula
$$f(r) \sim \frac{C}{r^\alpha}$$
Where $r$ is the rank and $\alpha$ is typically close to $1$.

## Implications for IR
- **Common Words**: A few words (stopwords) appear very frequently and provide little discriminative power.
- **Rare Words**: Most words appear very rarely, making them highly discriminative but prone to sparsity.
- **Weighting**: This law justifies the use of [[TF-IDF]], which penalizes high-frequency terms (via IDF).

See also: [[TF-IDF]], [[Stopwords]]
