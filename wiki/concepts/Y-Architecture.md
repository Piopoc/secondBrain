# Y-Architecture

The **Y-Architecture** is the fundamental structural pattern of most Information Retrieval systems. It describes the separation between the offline indexing process and the online search process, which converge at the matching stage.

## The Two Branches
1. **Offline Branch (Indexing)**:
   - **Input**: Document Corpus.
   - **Process**: Documents are processed by an [[Lucene-Analyzer]] and written to an index via an [[Lucene-IndexWriter]].
   - **Output**: An inverted index (surrogate representation) stored on disk.
2. **Online Branch (Search)**:
   - **Input**: User Query.
   - **Process**: The query is processed by the **exact same** [[Lucene-Analyzer]] used during indexing.
   - **Output**: A query vector.

## The Convergence (Matching)
The two branches meet at the **Matching** stage, where the query vector is compared against the index using a relevance function (e.g., [[Cosine-Similarity]] or [[BM25]]) to produce a ranked list of documents.

**Critical Constraint**: Any change to the Analyzer (e.g., changing the stemmer) requires a full re-indexing of the corpus to maintain consistency between the two branches.

See also: [[Apache-Lucene]], [[Lucene-Analyzer]]
