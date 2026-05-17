---
date: 2026-05-08
source: [[raw/11/image2.png]]
tags: [statistics, sampling, quality-assurance]
---

# Stratified Sampling KG

Il **campionamento stratificato** è la tecnica utilizzata nel framework di valutazione orientato all'utility per ottimizzare l'allocazione del budget di annotazione in un Knowledge Graph.

## Procedura
Invece di un campionamento casuale semplice (naive), il KG viene partizionato in **strati (strata)** basati su una metrica di utility (es. popolarità nei query log):
1. **Definizione Strati**: Es. 5 quintili di popolarità.
2. **Stratificazione**: 
    - Strato 1: Fatti più popolari.
    - ...
    - Strato 5: Fatti meno popolari (long tail).
3. **Allocazione Budget**: Il budget di annotazione viene distribuito tra gli strati per massimizzare la precisione della stima dell'accuratezza percepita.

## Vantaggi
- Riduce la varianza della stima globale.
- Garantisce che le entità più critiche (popolari) siano validate con maggiore precisione.
- Permette di gestire budget di annotazione limitati in modo efficiente.

Vedi anche: [[Utility_KG]], [[Valutazione_Qualita_KG]], [[Lezione_28_Knowledge_Graphs]]
