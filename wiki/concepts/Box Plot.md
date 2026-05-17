---
date: 2026-05-08
source: [[raw/10/image0.png]]
tags: [statistics, data-visualization]
---

# Box Plot

Il **Box Plot** (o diagramma a scatola e baffi) è uno strumento grafico utilizzato per riassumere visivamente la distribuzione di un insieme di dati.

## Utilità
È particolarmente utile per confrontare le performance di più sistemi su una collezione di query o topic, permettendo di identificare rapidamente la tendenza centrale, la dispersione e la presenza di valori anomali.

## Struttura
- **Q1 (25° percentile)**: Il valore sotto il quale si trova il 25% dei dati.
- **Mediana (Q2, 50° percentile)**: Il valore centrale della distribuzione.
- **Q3 (75° percentile)**: Il valore sotto il quale si trova il 75% dei dati.
- **IQR (Inter-Quartile Range)**: La differenza tra Q3 e Q1.
- **Whiskers**: Estensioni che arrivano fino a $1.5 \cdot IQR$ dai quartili.
- **Outliers**: Valori che superano i limiti dei baffi.

Vedi anche: [[IQR]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
