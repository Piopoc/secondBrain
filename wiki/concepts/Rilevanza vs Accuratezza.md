---
date: 2026-05-08
source: [[raw/11/image1.png]]
tags: [information-retrieval, accuracy, relevance]
---

# Rilevanza vs Accuratezza

Nel contesto dei Knowledge Graph e della ricerca di informazioni, è fondamentale distinguere tra la **rilevanza** di un dato e la sua **accuratezza**.

## Definizioni
- **Rilevanza**: La misura in cui un fatto risponde alla query dell'utente.
- **Accuratezza (Verità)**: La misura in cui un fatto corrisponde alla realtà dei fatti.

## Il Problema nei Sistemi IR
I sistemi di Information Retrieval tradizionali sono progettati per massimizzare la rilevanza. Di conseguenza, possono restituire fatti che sono **altamente rilevanti ma falsi**.

**Esempio**:
- Query: "Premi vinti da Einstein"
- Fatto nel KG: `(Einstein, premio, Academy Award)`
- Analisi: Il fatto è *rilevante* (parla di premi di Einstein) ma è *falso* (Einstein non ha vinto l'Oscar).

Vedi anche: [[Entity_Card]], [[Valutazione_Qualita_KG]], [[Lezione_28_Knowledge_Graphs]]
