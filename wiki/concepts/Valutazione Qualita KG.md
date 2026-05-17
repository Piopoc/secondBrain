---
date: 2026-05-08
source: [[raw/11/image1.png]]
tags: [knowledge-graphs, quality-assurance, statistics]
---

# Valutazione Qualità KG

La valutazione della qualità di un Knowledge Graph (KG) consiste nel determinare la percentuale di fatti corretti presenti nella struttura.

## La Sfida dell'Annotazione
I KG reali (come DBpedia) contengono milioni di triple. L'annotazione manuale completa è impossibile (es. stima di 3.000 anni per DBpedia). È quindi necessario ricorrere a metodi di stima statistica.

## Approcci di Stima
1. **Campionamento Semplice (Naive)**:
    - Si estraggono $n$ fatti a caso e si calcola la percentuale di corretti.
    - **Limiti**: Rischio di campionamento distorto (bias verso fatti popolari) e mancanza di intervalli di confidenza.
2. **Stima Statistica con Garanzie**:
    - Utilizzo di stimatori non distorti.
    - Calcolo di intervalli di confidenza per definire l'affidabilità della stima.

## Stimatore dell'Accuratezza
L'accuratezza $\hat{\mu}$ è definita come la proporzione di fatti corretti:
$$\hat{\mu} = \frac{1}{N} \sum_{i=1}^N \mathbb{1}[\text{fatto}_i \text{ è corretto}] = \frac{\mathcal{T}}{\mathcal{M}}$$
dove $\mathcal{T}$ è il numero di fatti corretti e $\mathcal{M}$ la dimensione totale del KG.

Vedi anche: [[Rilevanza_vs_Accuratezza]], [[Lezione_28_Knowledge_Graphs]]
