---
date: 2026-05-08
source: [[raw/10/image4.png]]
tags: [statistics, power-analysis]
---

# Potenza Statistica (Power)

La **Potenza Statistica** (o Power) è la probabilità che un test statistico riesca a rigettare l'ipotesi nulla $H_0$ quando questa è effettivamente falsa. In termini semplici, è la probabilità di rilevare una differenza reale quando essa esiste.

## Formula
$$\text{Power} = 1 - \beta$$
dove $\beta$ è la probabilità di commettere un Errore di Tipo II.

## Come aumentare il Power
Il modo principale per aumentare la potenza di un test è **aumentare il numero di campioni** $n$ (es. più query o topic in IR). 

**Meccanismo**:
La test statistic $t_{stat}$ è proporzionale a $\sqrt{n}$:
$$t_{stat} = \frac{\hat{\mu}_D}{\sqrt{\hat{\sigma}_D^2/n}}$$
All'aumentare di $n$, $t_{stat}$ cresce, rendendo più probabile che superi il valore critico $t_{crit}$ e porti al rigetto di $H_0$.

## Rischio: Significatività vs Rilevanza
Con campioni estremamente grandi ($N$ enorme), è possibile ottenere risultati **statisticamente significativi** (p-value molto basso) anche per differenze minime che sono **praticamente irrilevanti**. Questo fenomeno è legato al rischio di *p-hacking*.

Vedi anche: [[Errori_Statistici]], [[Test_Statistic]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
