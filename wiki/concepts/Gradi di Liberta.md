---
date: 2026-05-08
source: [[raw/10/image5.png]]
tags: [statistics, theory]
---

# Gradi di Libertà

In statistica, i **gradi di libertà** (df, *degrees of freedom*) rappresentano il numero di valori in un calcolo finale che sono liberi di variare.

## Il caso $n-1$ nel t-test
Nel calcolo della varianza campionaria $\hat{\sigma}_D^2$, si utilizzano $n-1$ gradi di libertà invece di $n$. 

**Perché?**
Perché per calcolare la varianza è necessario conoscere preventivamente la media campionaria $\hat{\mu}_D$. L'uso della media impone un vincolo lineare ai dati: la somma degli scostamenti dalla media deve essere sempre zero ($\sum (d_i - \hat{\mu}_D) = 0$). 
Di conseguenza, se conosciamo $n-1$ valori e la media, l'ultimo valore è deterministicamente fissato. Solo $n-1$ valori sono quindi "liberi" di variare.

Vedi anche: [[t-test_di_Student_Paired]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
