---
date: 2026-05-08
source: [[raw/10/image3.png]]
tags: [statistics, probability]
---

# p-value

Il **p-value** è la probabilità di osservare una test statistic almeno altrettanto estrema di quella ottenuta, assumendo che l'ipotesi nulla ($H_0$) sia vera.

## Formula
$$p\text{-value} = P(|T| \ge |t_{stat}|, H_0)$$

## Interpretazione
Il p-value viene confrontato con il livello di significatività $\alpha$:
- **$p\text{-value} < \alpha$**: Si rigetta $H_0 \rightarrow$ la differenza è statisticamente significativa.
- **$p\text{-value} \ge \alpha$**: Non si rigetta $H_0 \rightarrow$ la differenza non è significativa.

## Perché è preferito al Valore Critico?
1. **Auto-contenuto**: È una probabilità (0-1), quindi direttamente interpretabile senza conoscere i parametri della distribuzione.
2. **Portabile**: Il lettore può applicare il proprio $\alpha$ preferito senza ricalcolare tutto.
3. **Informativo**: Permette di graduare la significatività (es. un p-value di 0.003 è molto più forte di uno di 0.04, anche se entrambi rigettano $H_0$ con $\alpha=0.05$).

Vedi anche: [[Livello_di_Significativita]], [[Test_Statistic]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
