---
date: 2026-05-08
source: [[raw/11/image1.png]]
tags: [summarization, knowledge-graphs]
---

# Dynamic Entity Summarization

La **Dynamic Entity Summarization** è il processo di selezione e ordinamento dei top-K fatti più importanti da mostrare in un Knowledge Panel per rappresentare un'entità.

## Caratteristiche
1. **Dinamicità**: A differenza di un riassunto statico, il ranking dei fatti cambia in base alla **query corrente**. Fatti diversi diventano rilevanti a seconda di cosa l'utente sta cercando.
2. **Obiettivo**: Fornire l'informazione più utile e concisa possibile.

## Sfide di Ottimizzazione
Il sistema deve bilanciare tre criteri spesso in conflitto:
- **Rilevanza**: I fatti devono rispondere alla query.
- **Diversità**: I fatti non devono essere ridondanti, ma coprire diversi aspetti dell'entità.
- **Accuratezza**: I fatti selezionati devono essere veri.

Vedi anche: [[Entity_Card]], [[Rilevanza_vs_Accuratezza]], [[Lezione_28_Knowledge_Graphs]]
