# 📚 Information Retrieval - Course Index

Questo indice mappa l'intero percorso del corso di Information Retrieval, integrando le lezioni teoriche e gli approfondimenti tecnici.

## 🛠️ Moduli Principali
- [[Fondamenti e Pipeline]]: Definizione di IR, confronto con DBMS, l'architettura a Y e l'intera pipeline di analisi testuale (Tokenizzazione $\rightarrow$ Stemming $\rightarrow$ Rappresentazione).
- [[Modelli di Recupero]]: Studio dei modelli matematici per il matching:
	- Boolean-Model
	- Vector-Space-Model e TF-IDF
	- Relevance Feedback (Rocchio Algorithm)
	- Modelli Probabilistici (Binary Independence Model, BM25)
	- Language Models (Unigram, Smoothing di Jelinek-Mercer Smoothing e Dirichlet Smoothing)
- [[Neural IR and Embeddings]]: Word Embeddings (Static vs Contextual), Transformer architecture, BERT, and Neural IR models (Cross-encoders, Bi-encoders, DPR, SPLADE).
- [[Valutazione Sperimentale]]: Il framework per misurare l'efficacia di un sistema:
	- Cranfield Paradigm
	- Processo di Pooling e Ground Truth
	- Metriche Set-based ($\text{Precision}$, $\text{Recall}$, $\text{F-measure}$)
	- Metriche Rank-based ($\text{P@K}$, $\text{MAP}$, $\text{nDCG}$, $\text{RBP}$)
- [[Implementazione Lucene]]: Guida pratica all'uso di Apache Lucene:
	- Componenti Core (`Analyzer`, `IndexWriter`, `IndexSearcher`)
	- Ottimizzazione della memoria e Thread-safety
	- Software Engineering per il parsing di grandi corpora (TIPSTER, MS MARCO)
- [[Privacy e Obfuscation]]: Tecniche per la protezione della privacy nelle query:
	- Differential Privacy (DP)
	- K-anonymity
	- Calibrated Multivariate Perturbations (KCMP)
- [[Statistical Testing]] : Statistical testing, Box Plots and CLT for Search Engine evaluation.
- [[MATLAB t-test TREC]]: Practical implementation of paired t-test on TREC datasets using MATLAB.
- [[Knowledge Graphs]]: Introduction to Knowledge Graphs, RDF triples, and Entity-Oriented Search.
- [[Neural Networks Basics]]: Fondamenti di Logistic Regression, FFNN, RNN e Transformers.

## 📝 Risorse Pratiche
- [[IR-Exam-Simulation]]: Esercizi numerici simulati per il parziale (TF-IDF, Cosine Similarity, Metriche di Valutazione, BM25, LM).

## 🎓 Take-Home Messages Globali
- L'IR è una disciplina **empirica**: non esiste un algoritmo "corretto" a priori, ma si procede per baseline $\rightarrow$ analisi dei fallimenti $\rightarrow$ iterazione.
- Il bilanciamento tra **Precision** e **Recall** è il trade-off fondamentale di ogni scelta nella pipeline di indicizzazione.
- La coerenza tra fase di **Indexing** e fase di **Search** (stesso `Analyzer`) è critica per il funzionamento del sistema.
