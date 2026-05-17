# L'Evoluzione del Recupero Informativo: Dal Determinismo alla Semantica

Questa sintesi analizza la traiettoria evolutiva dell'Information Retrieval (IR), evidenziando come il passaggio tra diversi modelli matematici sia stato guidato dalla necessità di risolvere il trade-off tra **Precision** e **Recall**.

## 1. L'Era del Determinismo: Il Modello Booleano
All'origine, l'IR era visto come un'estensione dei database. Il [[Modelli di Recupero#1. Boolean-Model (Bool. Mod.)]] operava su una logica binaria: un documento o soddisfaceva la query o non lo faceva.
- **Il Problema**: Questo approccio generava l'effetto "tutto o niente". Query troppo strette (AND) portavano a una $\text{Recall}$ bassissima; query troppo ampie (OR) a una $\text{Precision}$ inaccettabile.
- **Il Limite**: L'assenza di un **Ranking**. L'utente riceveva un "secchio" di documenti senza alcuna guida su quale fosse il più rilevante.

## 2. L'Introduzione della Rilevanza: VSM e TF-IDF
Il salto qualitativo avviene con il Vector Space Model (VSM). Qui l'IR smette di essere una questione di "set" e diventa una questione di **geometria**.
L'introduzione del [[concepts/TF-IDF]] ha permesso di dare un "peso" ai termini, riconoscendo che non tutte le parole hanno lo stesso potere discriminante.
- **L'Innovazione**: La similarità cosinuso ha trasformato la ricerca in un calcolo di distanza. Per la prima volta, è stato possibile ordinare i risultati.
- **Il Risultato**: La $\text{Precision}$ è migliorata drasticamente perché i documenti "più vicini" alla query venivano presentati per primi.

## 3. La Svolta Probabilistica: BM25 e Language Models
Nonostante il VSM, rimaneva un problema: la frequenza di un termine non cresce linearmente con la sua rilevanza (saturazione).
I modelli probabilistici, come il **BM25**, hanno introdotto la nozione di "probabilità di rilevanza".
- **La Logica**: Invece di misurare solo la distanza, questi modelli cercano di stimare la probabilità che un documento sia rilevante dato il comportamento statistico del corpus.
- **L'Impatto**: L'introduzione della normalizzazione della lunghezza del documento ha risolto il bias verso i documenti più lunghi, rendendo il ranking molto più equo e preciso.

## 4. Il Salto Semantico: Neural IR e Embeddings
L'ultimo passaggio, descritto in [[Implementazione Lucene#4. Dataset e Tooling]], è il passaggio dai termini alle **idee**.
Mentre i modelli precedenti (anche il BM25) soffrivano del problema del *vocabulary mismatch* (se cerco "cane" non trovo "cucciolo"), i modelli neurali utilizzano gli **Embedding**.
- **La Sintesi**: Trasformando le parole in vettori densi in uno spazio semantico, il sistema non cerca più la "parola", ma il "concetto".
- **Il Trade-off**: Abbiamo guadagnato una $\text{Recall}$ immensa (capacità di trovare documenti semanticamente correlati ma lessicalmente diversi), ma abbiamo introdotto una complessità computazionale enorme e una minore trasparenza (il "black box" dei modelli neurali).

## 🏁 Conclusione: Il Ciclo di Cranfield
L'intera evoluzione descritta sopra non sarebbe stata possibile senza il [[concepts/Cranfield-Paradigm]]. La capacità di misurare oggettivamente l'efficacia tramite $\text{MAP}$ e $\text{nDCG}$ ha permesso ai ricercatori di capire esattamente dove i modelli fallivano, spingendo l'IR a evolversi da semplice "filtro di parole" a vero e proprio "sistema di comprensione del bisogno informativo".
