# Stemming

**Stemming** is the process of reducing inflected or derived words to their word stem, also known as a root form.

## Objective
The goal is to improve **Recall** by grouping different morphological variations of the same word (e.g., "fishing", "fished", and "fisher" all map to "fish").

## The Stemming Trade-off
- **Over-stemming**: Occurs when words with different meanings are reduced to the same stem $\rightarrow$ **Decreases Precision**.
- **Under-stemming**: Occurs when related words are not grouped together $\rightarrow$ **Decreases Recall**.

## Common Algorithms
- [[Porter-Stemmer]]: Rule-based, removes the longest suffix.
- [[Lovins-Stemmer]]: Uses a list of suffixes and conversion rules.
- [[Krovetz-Stemmer]]: Hybrid approach using a dictionary.
- [[SPLIT-Stemmer]]: Statistical, unsupervised approach using prefix/suffix graphs.

See also: [[Lucene-Analyzer]], [[Recall]], [[Precision]]
