---
date: 2026-05-08
source: [[raw/11/image2.png]]
tags: [knowledge-graphs, utility, evaluation]
---

# Utility nei Knowledge Graph

Il concetto di **Utility** riconosce che non tutti i fatti all'interno di un Knowledge Graph hanno la stessa importanza per l'utente finale.

## Asimmetria della Popolarità
La distribuzione delle query verso le entità di un KG è fortemente asimmetrica:
- **Entità Popolari**: Una piccola frazione di entità (es. Einstein, Messi) riceve la stragrande maggioranza delle query.
- **Long Tail**: La maggior parte delle entità è cercata raramente.

## Implicazioni per la Qualità
Poiché le entità popolari sono quelle più esposte agli utenti, l'accuratezza di questi fatti ha un impatto molto più alto sulla percezione della qualità del sistema rispetto ai fatti della long tail. Pertanto, l'attenzione nella valutazione e correzione deve essere proporzionale all'utility (popolarità) dell'entità.

Vedi anche: [[Stratified_Sampling_KG]], [[Lezione_28_Knowledge_Graphs]]
