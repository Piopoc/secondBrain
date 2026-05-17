---
date: 2026-05-08
source: [[raw/11/image2.png]]
tags: [statistics, quality-assurance]
---

# Intervalli di Confidenza (KG Accuracy)

L'**intervallo di confidenza** è uno strumento statistico utilizzato per esprimere l'incertezza legata a una stima dell'accuratezza di un Knowledge Graph.

## Definizione
Invece di fornire un singolo valore (stima puntuale $\hat{\mu}$), l'intervallo di confidenza fornisce un range $[\hat{\mu} - \epsilon, \hat{\mu} + \epsilon]$ entro il quale si ritiene che risieda il valore vero $\mu$ con una determinata probabilità $(1-\alpha)$.

## Formula per l'Accuratezza
Per una proporzione di fatti corretti $\hat{\mu}$ in un campione di dimensione $n$:
$$CL = \hat{\mu} \pm z_{\alpha/2} \cdot \sqrt{\frac{\hat{\mu}(1-\hat{\mu})}{n}}$$

## Interpretazione Corretta
Se un KG ha un'accuratezza del 75% $\pm$ 3% con confidenza 95%, significa che:
- **SÌ**: Se ripetessimo il campionamento molte volte, il 95% degli intervalli calcolati conterrebbe l'accuratezza vera.
- **NO**: Non significa che il 95% dei fatti del KG si trova in quell'intervallo.

Vedi anche: [[Valutazione_Qualita_KG]], [[Lezione_28_Knowledge_Graphs]]
