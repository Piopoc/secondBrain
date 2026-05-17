# IR - Implementazione Lucene

## 1. Apache Lucene Overview
**[[Apache-Lucene]]** è una libreria Java open-source per l'indicizzazione e la ricerca. Non è un server di ricerca completo, ma il "motore" che alimenta sistemi come **[[Apache Solr]]** ed **[[Elasticsearch]]**.

### [[Y-Architecture]] (Dettaglio Tecnico)
L'implementazione segue una separazione netta tra la costruzione dell'indice e la sua interrogazione.

#### 🌑 Fase Offline: Indexing
1. **Document & Field**: Un `Document` è un contenitore di `Field`. I campi possono essere:
	- `Indexed`: Ricercabili.
	- `Stored`: Salvati raw su disco per essere mostrati all'utente.
	- `Tokenized`: Processati dall'Analyzer.
2. **Analyzer**: Orchestra la pipeline di trasformazione del testo.
3. **IndexWriter**: Scrive i dati nell'indice. È l'unico componente che può modificare l'indice.

#### ☀️ Fase Online: Search
1. **QueryParser**: Trasforma la stringa di testo in un oggetto `Query`.
2. **IndexSearcher**: Interroga l'indice e restituisce una lista di `ScoreDoc` (documenti con il loro punteggio di rilevanza).
3. **Directory**: Astrazione del filesystem dove risiede l'indice.

### L'Indice Invertito (Inverted Index)
Il risultato finale della pipeline è l'**[[Inverted Index]]**. Invece di mappare `Documento` $\rightarrow$ `Termini`, l'indice invertito mappa `Termine` $\rightarrow$ `Lista di Documenti` che lo contengono. Questa struttura è ciò che permette ai modelli di recupero di operare in tempi millisecondi anche su milioni di documenti.

---

## 2. Internals e Performance

### Immutabilità e Segmenti
L'indice di Lucene non è un unico file monolitico, ma è composto da **segmenti immutabili**.
- **Vantaggio**: Permette un caching estremamente efficiente.
- **Conseguenza**: Per aggiornare un documento, Lucene ne scrive una nuova versione in un nuovo segmento e marca la vecchia come "eliminata". Periodicamente, i segmenti vengono uniti (**Merge**).

### Thread-Safety
- **IndexSearcher**: È thread-safe. Molteplici thread possono eseguire ricerche contemporaneamente sullo stesso indice.
- **IndexWriter**: **NON** è thread-safe per la scrittura. Lucene proibisce la scrittura simultanea sullo stesso indice per evitare corruzioni.

### Ottimizzazione della Memoria
Per evitare l'overhead della Garbage Collection durante il processamento di milioni di token:
- **Attribute System**: Lucene non passa oggetti `Token` tra i filtri, ma usa un set di attributi condivisi (es. `CharTermAttribute`) che vengono modificati *in-place*.
- **StringBuilder**: All'interno dei custom `TokenFilter`, è fondamentale usare `StringBuilder` invece della concatenazione di stringhe (`+`), per evitare l'allocazione massiva di oggetti temporanei.

---

## 3. Software Engineering per l'IR

### Parsing di Corpora Massivi
Quando si processano dataset come **[[MS MARCO]]** o **[[TIPSTER]]**, è impossibile caricare tutto in memoria.
- **Pattern Iterator/Iterable**: I parser devono implementare interfacce iterative per processare un documento alla volta.
- **Java Reflection**: Per rendere il sistema modulare, si usa `Class.forName()` per istanziare dinamicamente il parser corretto (es. `TipsterParser` vs `MsmarcoParser`) basandosi su un file di configurazione.

### Gestione dell'Encoding
L'encoding dei caratteri è una delle cause principali di crash dei sistemi IR.
- **Evoluzione**: $\text{ASCII (7-bit)} \rightarrow \text{Extended ASCII (8-bit)} \rightarrow \text{Unicode/UTF-8}$.
- **UTF-8**: Risolve i conflitti regionali usando una lunghezza di byte variabile. È obbligatorio verificare l'encoding della collezione prima di iniziare l'indicizzazione per evitare token corrotti.

---

## 4. Dataset e Tooling
### Dataset di Riferimento
- **TIPSTER**: Documenti lunghi (articoli di news). Qui lo [[Stemming]] migliora significativamente la $\text{MAP}$.
- **MS MARCO**: Passaggi brevi (short passages). Qui i modelli sparsi (BM25) sono dominati dai **Neural Retrievers** (BERT embeddings), che raggiungono precisioni molto più alte ($\text{P@10} \approx 87\%$).

### Tooling
- **Lucene Luke**: GUI per ispezionare gli indici binari, verificare i conteggi dei token e testare le query in tempo reale.
- **`trec_eval`**: Tool standard per il calcolo delle metriche di valutazione.

## 🎓 Take-Home Message per lo Sviluppatore
L'IR è profondamente empirica. La strategia corretta è:
1. Costruire un **parser "stupido"** (dump di tutto il testo in un unico campo) per stabilire una **baseline**.
2. Eseguire un'analisi dei fallimenti (**failure analysis**).
3. Aggiungere complessità (custom analyzers, stemming, neural re-ranking) solo se i dati dimostrano un miglioramento della $\text{MAP}$ o della $\text{nDCG}$.
