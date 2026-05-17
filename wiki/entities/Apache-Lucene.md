# Apache Lucene

**Apache Lucene** is a high-performance, full-featured text search engine library written in Java. It is not a standalone server but a library that provides the core indexing and searching capabilities.

## Core Architecture
Lucene implements the **Y-Architecture**, separating the indexing and searching phases.

### Key Components
- **Analyzer**: The pipeline that transforms raw text into tokens (Tokenization $\rightarrow$ Stopword Removal $\rightarrow$ Stemming).
- **IndexWriter**: The component responsible for creating and updating the inverted index.
- **IndexSearcher**: The component used to query the index and retrieve ranked results.
- **Directory**: An abstraction of the filesystem where the index is stored.

## Key Technical Features
- **Immutability**: The index is composed of immutable **segments**. Updates are handled by writing new segments and marking old documents as deleted.
- **Merge Process**: Periodically, Lucene merges small segments into larger ones to optimize search performance.
- **Attribute System**: Uses a shared attribute system to avoid massive object allocation during tokenization, reducing Garbage Collection overhead.

## Ecosystem
Lucene serves as the core engine for many popular search servers, most notably **Apache Solr** and **Elasticsearch**.

See also: [[concepts/Y-Architecture]], [[concepts/Lucene-Analyzer]]
