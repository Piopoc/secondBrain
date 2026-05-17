---
date: 2026-05-08
source: [[raw/10/image8.png]]
tags: [statistics, variance-analysis]
---

# ANOVA (Analysis of Variance)

L'**ANOVA** è un metodo statistico utilizzato per confrontare le medie di tre o più gruppi (sistemi) contemporaneamente. L'obiettivo è determinare se esiste una differenza statisticamente significativa tra almeno due di queste medie, evitando l'inflazione dell'errore tipica delle comparazioni multiple.

## Logica Fondamentale
L'ANOVA scompone la varianza totale dei dati in due componenti:
1. **Effetto Sistema (Between-group variance)**: Varianza dovuta alla differenza tra le medie dei vari sistemi.
2. **Effetto Errore (Within-group variance)**: Varianza residua dovuta al rumore o alla variabilità intrinseca dei topic.

$$\text{Varianza Totale} = \text{Effetto Sistema} + \text{Effetto Errore}$$

## Meccanica del Test
- **Sum of Squares (SS)**: Si calcolano le somme dei quadrati per l'effetto totale ($SS_{tot}$), il sistema ($SS_{system}$) e l'errore ($SS_{error}$).
- **Mean Squares (MS)**: Si divide la SS per i rispettivi gradi di libertà ($DF$):
    - $MS_{system} = SS_{system} / (q-1)$
    - $MS_{error} = SS_{error} / (pq-q)$
- **F-test**: La statistica $F_{stat} = \frac{MS_{system}}{MS_{error}}$ segue una distribuzione F di Snedecor. Se $F_{stat} > F_{crit}$, si rigetta l'ipotesi nulla $H_0$ (che assume che tutte le medie siano uguali).

## Assunzioni
L'ANOVA richiede che i dati soddisfino:
- **Indipendenza**: I campioni devono essere indipendenti.
- **Normalità**: I dati devono seguire una distribuzione normale.
- **Omoschedasticità**: Le varianze tra i gruppi devono essere approssimativamente uguali.

Vedi anche: [[F-test]], [[Tukey_HSD_Test]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
