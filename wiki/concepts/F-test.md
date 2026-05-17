---
date: 2026-05-08
source: [[raw/10/image8.png]]
tags: [statistics, hypothesis-testing]
---

# F-test

L'**F-test** è il test statistico utilizzato nell'ambito dell'ANOVA per determinare se la varianza tra i gruppi è significativamente maggiore della varianza all'interno dei gruppi.

## Formula
La statistica F è definita come il rapporto tra i quadrati medi (Mean Squares):
$$F_{stat} = \frac{MS_{system}}{MS_{error}}$$

## Interpretazione
- Se $F_{stat}$ è vicino a 1, la varianza tra i sistemi è simile a quella dell'errore $\rightarrow$ non c'è evidenza di differenze tra le medie.
- Se $F_{stat}$ è significativamente maggiore di 1, l'effetto del sistema domina l'errore $\rightarrow$ si rigetta $H_0$ e si conclude che almeno due medie sono diverse.

La distribuzione di riferimento è la **Distribuzione F di Snedecor**, con gradi di libertà $(DF_{system}, DF_{error})$.

Vedi anche: [[ANOVA]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
