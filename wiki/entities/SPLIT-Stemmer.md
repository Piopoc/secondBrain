# SPLIT-Stemmer

The **SPLIT Stemmer** is a statistical, unsupervised stemming approach.

## Mechanism
Instead of using predefined rules, it analyzes the corpus to find common prefixes and suffixes. It builds a graph where:
- **Nodes**: Prefixes and suffixes.
- **Edges**: Complete words.

This allows the system to discover stemming patterns automatically based on the actual data.

See also: [[Stemming]]
