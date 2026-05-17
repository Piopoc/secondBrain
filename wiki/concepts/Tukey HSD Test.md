---
date: 2026-05-08
source: [[raw/10/image8.png]]
tags: [statistics, post-hoc]
---

# Tukey HSD Test

Il **Tukey HSD (Honestly Significant Difference)** è un test post-hoc utilizzato dopo che un'ANOVA ha mostrato un risultato significativo. Mentre l'ANOVA dice *che* esiste una differenza, il test di Tukey identifica *quali* coppie di medie sono significativamente diverse.

## Vantaggi
A differenza di una serie di t-test con correzione di Bonferroni, il test di Tukey è progettato specificamente per confrontare tutte le possibili coppie di medie mantenendo il tasso di errore di Tipo I (FWER) costante a $\alpha$.

## Meccanica
Il test calcola un intervallo di confidenza per la differenza tra ogni coppia di medie. Se la differenza tra due medie supera la soglia HSD, la coppia è considerata significativamente diversa.

La formula coinvolge la distribuzione del **range studentizzato** (Studentized Range Distribution) $q_{\alpha, q, n}$:
$$HSD = q_{\alpha, q, n} \cdot \sqrt{\frac{MS_{error}}{n}}$$

Vedi anche: [[ANOVA]], [[Family_Wise_Error_Rate]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
