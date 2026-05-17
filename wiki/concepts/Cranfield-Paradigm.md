# Cranfield Paradigm

The **Cranfield Paradigm** is the gold standard for experimental evaluation in Information Retrieval. It abstracts real-world search into a controlled laboratory setting to ensure that experiments are **repeatable** and **comparable**.

### The Triad
The paradigm relies on three essential components:
1. **Document Corpus**: A static set of documents.
2. **Topics**: Standardized representations of user information needs.
3. **Relevance Judgments (qrels)**: Human-verified labels indicating which documents are relevant to which topics.

### Significance
By fixing the corpus and the topics, researchers can test different algorithms (e.g., comparing BM25 vs. a Neural Retriever) on the exact same ground truth, allowing for a scientifically valid comparison of effectiveness.

See also: [[summaries/IR/IR - Valutazione Sperimentale#1. Il Paradigma di Cranfield]]
