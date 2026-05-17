# IR - Fondamenti e Pipeline

## 1. Definizione e Ambito
L'**[[Information-Retrieval]] (IR)** è il campo che si occupa della struttura, analisi, organizzazione, storage, ricerca e recupero di informazioni.

### 🎯 Obiettivo Principale
L'obiettivo è trovare gli **item più rilevanti** per soddisfare un bisogno informativo dell'utente.

### ⚖️ IR vs Database (DBMS)
Mentre i DB lavorano su dati strutturati e risposte deterministiche, l'IR opera in un contesto di ambiguità.

| Feature | Databases (DBMS) | Information Retrieval (IR) |
| :--- | :--- | :--- |
| **Tipo di Dato** | Strutturato (Schema, records) | Non strutturato / Semi-strutturato (Testo, media) |
| **Matching** | Exact match (Boolean/SQL) | Best match (Ranking, stima) |
| **World View** | Closed World (Se non c'è, non esiste) | Open World (Il sistema potrebbe semplicemente non trovarlo) |
| **Interazione** | One-shot query | Iterativa (Raffinamento della query) |
| **Valutazione** | Focalizzata sull'Efficienza (Velocità, scala) | Focalizzata sull'Effettività (Rilevanza) + Efficienza |

### 🔍 Intento di Ricerca (Search Intent)
- **Exploratory**: Query ampie con molti item potenzialmente rilevanti (es. "Cos'è l'IR?").
- **Known-Item / Precision-Oriented**: Query strette che mirano a un documento specifico.

---

## 2. [[Y-Architecture]] (L'Architettura a Y)
Il sistema di ricerca è diviso in due fasi distinte che convergono nel processo di matching.

### 🌑 Fase Offline (Indexing)
I documenti vengono processati per creare una **rappresentazione surrogata** (vettori) memorizzata su disco.
`Documenti` $\rightarrow$ `Analyzer` $\rightarrow$ `IndexWriter` $\rightarrow$ `Indice (Directory)`

### ☀️ Fase Online (Search)
La query dell'utente subisce lo **stesso identico processo di indicizzazione** per diventare un vettore comparabile.
`Query` $\rightarrow$ `Analyzer` $\rightarrow$ `Matching (Cosine Similarity / Dot Product)` $\rightarrow$ `Lista Ranked`

**⚠️ Nota Critica**: Se si cambia la configurazione dell'Analyzer (es. aggiungendo uno stemmer), è obbligatorio **re-indicizzare l'intero corpus**, altrimenti i termini della query non coincideranno con quelli dell'indice.

---

## 3. La Pipeline di Indicizzazione (Lexical Analysis)
Il testo grezzo viene trasformato in una rappresentazione indicizzabile attraverso una serie di step.

### A. [[Tokenization]]
Conversione del testo in un flusso di parole (**tokens**).
- **Processo**: Separazione tramite spazi e punteggiatura $\rightarrow$ conversione in lower case.
- **Pitfalls**: Una tokenizzazione semplicistica può distruggere entità critiche (acronimi, numeri, URL, lingue non occidentali come Cinese/Giapponese).

### B. Eliminazione delle [[Stopwords]]
Rimozione di parole ad alta frequenza e basso valore semantico (articoli, preposizioni).
- **Vantaggio**: Riduzione drastica della dimensione dell'indice e del footprint di memoria.
- **Rischio**: Può alterare il significato (es. "To be or not to be" diventerebbe vuoto).

### C. [[Stemming]] (Riduzione alla radice)
Processo per gestire plurali e variazioni sintattiche, riducendo le parole alla loro forma base (**stem**).
- **Over-stemming**: Parole con significati diversi vengono ridotte allo stesso stem $\rightarrow$ **Danneggia la Precision**.
- **Under-stemming**: Parole correlate non vengono raggruppate $\rightarrow$ **Danneggia la Recall**.

#### Tipologie di Stemmer (Dettagli Tecnici):
1. **[[Porter-Stemmer]]**: Algoritmo basato su regole che rimuove i suffissi (elimina il suffisso più lungo).
2. **[[Lovins-Stemmer]]**: Produce parole reali attraverso una lista di suffissi e regole di conversione.
3. **[[Krovetz-Stemmer]]**: Approccio ibrido algoritmico-dizionario. Se la parola è nel dizionario resta tale, altrimenti si cerca un suffisso rimuovibile.
4. **[[SPLIT-Stemmer]]**: Stemmer statistico non supervisionato. Divide ogni parola in tutti i possibili prefissi e suffissi, creando un grafo dove i nodi sono prefissi/suffissi e gli archi sono parole complete.

---

## 4. Rappresentazioni Avanzate

### [[N-Grams]]
Sequenze fisse di $n$ elementi consecutivi.
- **Word N-grams**: (Bigrams, Trigrams) Utili per catturare entità composte. Esplodono la dimensione dell'indice.
- **Character N-grams**: Finestra scorrevole di caratteri. Usati come fallback quando non esiste uno stemmer per una lingua. Rischio di falsi positivi se la dimensione non coincide con la lunghezza media dello stem (4-5 caratteri).

### Analisi Linguistica
- **[[POS-Tagging]] (Part-of-Speech)**: Uso di modelli statistici per predire la categoria sintattica (es. `VB` per verbo, `NN` per nome).
- **[[NER]] (Named Entity Recognition)**: Identificazione di entità di interesse (persone, luoghi). È un ramo dell'Information Extraction.

### Indici Sparse vs Dense

Il passaggio da rappresentazioni sparse a dense segna l'evoluzione dall'approccio **lessicale** (matching di parole) a quello **semantico** (matching di concetti).

#### 1. Rappresentazioni Sparse (L'era del Term Matching)
Si basano sulla **Matrice Termine-Documento**, dove ogni riga è un termine unico del vocabolario e ogni colonna è un documento.
- **Struttura**: Le celle contengono $0$ (assenza) o $1$ (presenza) del termine.
- **Perché "Sparse"?**: In un corpus reale, la stragrande maggioranza delle celle è zero (un documento usa solo una frazione minima del vocabolario totale).
- **Vantaggi**: Calcolo estremamente veloce tramite *dot product*.
- **Limite Fondamentale**: Il **[[Vocabulary-Mismatch]]**. Se l'utente cerca "auto" e il documento contiene "automobile", il sistema restituisce $0$ (non match), ignorando la correlazione semantica.

#### 2. Rappresentazioni Dense (L'era degli Embedding)
I documenti e le query sono proiettati in uno spazio vettoriale a dimensione fissa (es. 768 dimensioni per i modelli BERT).
- **Struttura**: Ogni dimensione non corrisponde più a una parola, ma a una "caratteristica semantica" astratta. Le celle contengono numeri reali (es. $0.12, -0.45, 0.88$).
- **Perché "Dense"?**: Non ci sono zeri; ogni dimensione contribuisce a definire il concetto.
- **Vantaggi**: Risolve il vocabulary mismatch. Parole simili finiscono in posizioni vicine nello spazio vettoriale, permettendo di trovare documenti rilevanti anche senza parole in comune.
- **Svantaggi**: Costo computazionale molto più elevato (moltiplicazioni di matrici dense) e minore trasparenza (è difficile capire *perché* due vettori siano vicini).

