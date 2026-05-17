---
date: 2026-05-08
source: [[raw/10/image5.png]]
tags: [statistics, multiple-comparisons]
---

# Correzione di Bonferroni

La **Correzione di Bonferroni** è il metodo più semplice per mitigare il problema dell'inflazione dell'errore (FWER) quando si effettuano comparazioni multiple.

## Metodo
Invece di utilizzare il livello di significatività $\alpha$ per ogni singolo test, si utilizza una soglia corretta $\alpha'$:
$$\alpha' = \frac{\alpha}{m}$$
dove $m$ è il numero di comparazioni effettuate.

## Analisi Critica
Sebbene efficace nel ridurre i Falsi Positivi (Errore di Tipo I), la correzione di Bonferroni presenta due limiti principali:
1. **Eccessivamente Conservativa**: Rende molto difficile rigettare l'ipotesi nulla.
2. **Aumento Errori di Tipo II**: Aumenta significativamente la probabilità di commettere Falsi Negativi (non rilevare una differenza reale).

Vedi anche: [[Family_Wise_Error_Rate]], [[Errori_Statistici]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
