---
date: 2026-05-08
source: [[raw/10/image5.png]]
tags: [statistics, hypothesis-testing]
---

# t-test di Student (Paired)

Il **t-test di Student appaiato** è un test statistico utilizzato per determinare se esiste una differenza significativa tra le medie di due gruppi correlati (es. due sistemi di IR testati sugli stessi topic).

## Assunzioni Fondamentali
Perché il test sia valido, devono essere soddisfatte tre condizioni:
1. **Indipendenza**: Il campione deve essere casuale.
2. **Normalità**: Le due variabili devono seguire una distribuzione normale.
3. **Omoschedasticità**: Le due distribuzioni devono avere la stessa varianza (sconosciuta).

## Formulazione Matematica
Il test si basa sull'analisi delle differenze $D_i = X_i - Y_i$ per ogni coppia $i$.

1. **Media delle differenze**: $\hat{\mu}_D = \frac{1}{n} \sum_{i=1}^n d_i$
2. **Varianza delle differenze**: $\hat{\sigma}_D^2 = \frac{1}{n-1} \sum_{i=1}^n (d_i - \hat{\mu}_D)^2$
3. **Test Statistic**: 
   $$t_{stat} = \frac{\hat{\mu}_D}{\sqrt{\hat{\sigma}_D^2/n}}$$

## Distribuzione e Decisione
La statistica $t_{stat}$ segue una **distribuzione t di Student** con $n-1$ gradi di libertà. Il risultato viene confrontato con il valore critico $t_{crit}(n-1, \alpha/2)$ per decidere se rigettare $H_0$.

### Confronto con il Teorema del Limite Centrale (CLT)
Sebbene la formula della test statistic sia identica, la differenza risiede nella varianza utilizzata:
- **CLT**: Utilizza la varianza della **popolazione** ($\sigma$, nota) $\rightarrow$ converge a una distribuzione **Normale**.
- **t-test**: Utilizza la varianza **campionaria** ($\hat{\sigma}$, stimata) $\rightarrow$ converge a una distribuzione **t di Student**.
- Per $n \to \infty$, la distribuzione t converge alla normale.

Vedi anche: [[Gradi_di_Liberta]], [[Omoschedasticita]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
