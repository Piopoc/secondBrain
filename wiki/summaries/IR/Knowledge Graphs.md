---
date: 2026-05-08
source: [[raw/11/image0.png]]
tags: [knowledge-graphs, entity-search, information-retrieval]
---

# Sintesi: Knowledge Graphs & Entity-Oriented Search (Lezione 28)

Questa lezione introduce i [[concepts/Knowledge Graph|Knowledge Graph (KG)]] come strutture per rappresentare la conoscenza in modo strutturato e il loro impiego nei moderni motori di ricerca per l'estrazione di entità e la generazione di riassunti.

## 1. Knowledge Graph (KG)
Un **Knowledge Graph** è una struttura dati che rappresenta la conoscenza come una rete composta da **entità** (nodi) e **relazioni** (archi).

**Modello a Triple**: La conoscenza è espressa tramite [[concepts/RDF Triple|triple]] $(s, p, o)$:
- **Soggetto (s)**: Un'entità o un blank node.
- **Predicato (p)**: La relazione che lega il soggetto all'oggetto.
- **Oggetto (o)**: Un'entità, un attributo o un blank node.

**Esempi di KG reali**:
- **DBpedia**: Versione strutturata di Wikipedia. Vedi [[entities/DBpedia_Wikidata]].
- **Wikidata**: KG collaborativo di Wikimedia. Vedi [[entities/DBpedia_Wikidata]].
- **Freebase**: (Ora integrato in Google Knowledge Graph).
- **Altri**: YAGO, ConceptNet, schema.org.

**Utilizzi principali**:
- **Information Retrieval**: Favorire la ricerca verso fatti validati.
- **Item Recommendation**: Pesare le raccomandazioni in base alla veridicità dei fatti.
- **Question Answering**: Permettere ricerche accurate su fatti specifici.

## 2. Entity-Oriented Search e Summarization
L'approccio orientato alle entità sposta il focus dalle parole chiave alle entità del mondo reale.

**Entity Card (Knowledge Panel)**:
L'[[concepts/Entity Card|Entity Card]] è il pannello laterale (tipico di Google) che appare durante la ricerca di un'entità. Viene costruito a partire da un KG e aggrega i fatti più rilevanti.

**Dynamic Entity Summarization**:
La [[concepts/Dynamic Entity Summarization|Dynamic Entity Summarization]] è il task di selezionare e ordinare i **top-K fatti** più importanti per rappresentare un'entità.
- **Dinamicità**: Il ranking non è statico, ma cambia in base alla query corrente.
- **Sfida**: Bilanciare tre dimensioni: **rilevanza**, **diversità** e **accuratezza/qualità** dei fatti.

**Rilevanza vs Verità (Accuratezza)**:
Un punto critico è che i sistemi di IR tradizionali ordinano i fatti per **rilevanza** rispetto alla query, non per **accuratezza**. Vedi [[concepts/Rilevanza vs Accuratezza]].
- Un fatto può essere *rilevante* (risponde alla query) ma *falso* (non è vero nel mondo reale).
- I sistemi tradizionali tendono a restituire fatti rilevanti, non necessariamente veri.

## 3. Valutazione della Qualità dei Knowledge Graph
I KG reali possono contenere una percentuale significativa di errori. Vedi [[concepts/Valutazione Qualita KG]].

**Il problema dell'annotazione**:
L'annotazione manuale completa è impossibile (es. validare DBpedia richiederebbe circa 3.000 anni di lavoro umano).

**Approcci di stima dell'accuratezza**:
1. **Campionamento Semplice (Naive)**: Si estraggono $n$ fatti a caso.
    - *Limiti*: Rischio di campionamento distorto e assenza di intervalli di confidenza.
2. **Stima Statistica con Garanzie**: Utilizzo di stimatori non distorti accompagnati da [[concepts/Intervalli di Confidenza KG|intervalli di confidenza]].

**Proprietà di un buon stimatore**:
- **Non distorto (unbiased)**: La media converge al valore vero.
- **Intervallo di Confidenza (CL)**: Fornisce un range con garanzia probabilistica $(1-\alpha)$.

**Il concetto di Utility e il Framework di Valutazione**:
L'attenzione nella valutazione deve essere proporzionale all'[[concepts/Utility KG|utility]] (popolarità) dell'entità.

**Framework di Valutazione Orientato all'Utility (Marchesin et al.)**:
Per ottimizzare il budget di annotazione, si segue un processo di [[concepts/Stratified Sampling KG|campionamento stratificato]] basato sulla popolarità.

**Risultati Sperimentali su DBpedia**:
L'analisi ha rivelato che **popolarità e qualità sono ortogonali**: le entità più popolari non sono né le più accurate né le meno accurate.

**Qualità vs Rilevanza nel Re-ranking**:
È possibile costruire sistemi più affidabili (più accurati) mantenendo le stesse prestazioni di rilevanza.

**Stimatore dell'Accuratezza**:
L'accuratezza $\hat{\mu}$ è definita come la proporzione di fatti corretti rispetto al totale:
$$\hat{\mu} = \frac{1}{N} \sum_{i=1}^N \mathbb{1}[\text{fatto}_i \text{ è corretto}] = \frac{\mathcal{T}}{\mathcal{M}}$$
dove $\mathcal{T}$ è il numero di fatti corretti e $\mathcal{M}$ la dimensione del KG.
