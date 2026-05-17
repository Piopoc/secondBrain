# Guida Completa al Recupero dell'Informazione (IR)

Questa sintesi raccoglie i pilastri fondamentali dell'Information Retrieval, partendo dalle basi infrastrutturali fino ai modelli di recupero moderni e alle tecniche di valutazione.

---

## 1. L'Infrastruttura: Pipeline di Analisi e Indice Invertito

Prima di poter applicare qualsiasi modello di matching, il testo grezzo deve essere trasformato in una forma strutturata. Questo processo è gestito da una **Pipeline di Analisi (Analyzer)**.

### La Pipeline di Preprocessing
Il testo passa attraverso diverse fasi per eliminare il rumore e normalizzare i termini:
1. **Tokenization**: Il testo viene spezzato in unità minime chiamate *token* (solitamente parole).
2. **Case Folding**: Tutti i termini vengono convertiti in minuscolo per evitare che "Casa" e "casa" siano trattate come parole diverse.
3. **Rimozione delle Stopwords**: Vengono eliminate parole estremamente comuni (articoli, preposizioni come "il", "di", "lo") che non aggiungono valore semantico e occuperebbero spazio inutilmente nell'indice.
4. **Stemming**: I termini vengono ridotti alla loro radice (es. "programmazione" $\rightarrow$ "program"). Questo permette di recuperare documenti che usano flessioni diverse della stessa parola.

**Regola d'oro**: L'analyzer usato per l'indicizzazione dei documenti deve essere identico a quello usato per l'analisi della query; diversamente, i termini non coincideranno mai.

### L'Indice Invertito (Inverted Index)
Il cuore tecnologico di ogni motore di ricerca è l'**Indice Invertito**. Invece di mappare ogni documento ai suoi termini, l'indice mappa ogni **termine** a una lista di **documenti** che lo contengono (Posting List). Questa struttura permette di trovare istantaneamente tutti i documenti rilevanti per una query senza dover scansionare l'intero corpus.

---

## 2. Il Modello Spaziale Vettoriale (VSM) e TF-IDF

Il **Vector Space Model (VSM)** rappresenta documenti e query come vettori in uno spazio multi-dimensionale, dove ogni dimensione corrisponde a un termine unico del vocabolario.

### La Pesatura TF-IDF
Non tutte le parole sono ugualmente utili per distinguere un documento. Il TF-IDF risolve questo problema combinando due metriche:
- **TF (Term Frequency)**: Misura quanto un termine è frequente in un documento. Se una parola appare spesso, è probabile che il documento tratti quell'argomento.
- **IDF (Inverse Document Frequency)**: Misura quanto un termine è "raro" nell'intero corpus. Parole comuni (come "sistema") hanno un IDF basso, mentre parole rare (come "quantum") hanno un IDF alto.

Il peso finale $w_{ik} = tf_{ik} \cdot idf_i$ premia i termini che sono frequenti nel documento ma rari nel resto della collezione, identificandoli come i veri "descrittori" del contenuto.

### Cosine Similarity
Per misurare la rilevanza tra una query $\vec{q}$ e un documento $\vec{d}$, si calcola il **coseno dell'angolo $\theta$** tra i loro vettori. 
Perché il coseno? Perché a differenza della distanza euclidea, il coseno ignora la lunghezza dei vettori. Questo significa che un documento lungo e uno corto che trattano lo stesso argomento (stessa direzione del vettore) avranno una similarità alta, evitando che i documenti più lunghi vengano favoriti solo perché contengono più parole.

---

## 3. Modelli Probabilistici: BIM e BM25

Mentre il VSM è geometrico, i modelli probabilistici vedono l'IR come un problema di classificazione: "Qual è la probabilità che questo documento sia rilevante data la query?".

### Binary Independence Model (BIM)
Il BIM è il modello probabilistico più semplice. Assume che:
1. La presenza di un termine sia **binaria** (presente/assente).
2. I termini siano **indipendenti** tra loro.
Il punteggio di rilevanza è basato sul rapporto tra la probabilità che un termine appaia in un documento rilevante rispetto a uno non rilevante.

### BM25 (Best Match 25)
BM25 è l'evoluzione moderna del modello probabilistico e lo standard industriale. Risolve due limiti critici del TF-IDF:
1. **Saturazione della TF**: Nel TF-IDF, se una parola appare 100 volte, pesa molto più di se appare 10 volte. BM25 introduce una curva di saturazione: dopo un certo numero di occorrenze, l'importanza del termine smette di crescere significativamente.
2. **Normalizzazione della lunghezza**: BM25 penalizza i documenti eccessivamente lunghi che contengono molti termini solo per "estensione" e premia i documenti concisi che centrano l'argomento.

---

## 4. Modelli Linguistici (LM) e Smoothing

Nei **Language Models per l'IR**, un documento è visto come una distribuzione di probabilità su tutte le parole del linguaggio. La query è vista come una sequenza di parole che il modello del documento deve "generare".

### Il problema dello Zero e lo Smoothing
Se un termine della query non appare in un documento, la probabilità di generarlo è 0. Poiché il punteggio finale è spesso un prodotto di probabilità, un singolo termine mancante azzererebbe l'intera rilevanza del documento. Per evitare questo, si usa lo **Smoothing**:
- **Jelinek-Mercer Smoothing**: Combina la probabilità del documento con quella della collezione intera (background model) tramite un peso $\lambda$.
- **Dirichlet Smoothing**: Immagina di aggiungere al documento un numero di "parole virtuali" distribuite secondo la frequenza della collezione.

---

## 5. Valutazione del Sistema di Recupero

Come sappiamo se un sistema di IR funziona? Si usa il **Paradigma di Cranfield**, che prevede un test set composto da una collezione di documenti, un set di query e giudizi umani di "rilevanza" (Gold Standard).

### Metriche Fondamentali
- **Precision**: Quale percentuale dei documenti recuperati è effettivamente rilevante? (Evitare i falsi positivi).
- **Recall**: Quale percentuale di tutti i documenti rilevanti esistenti è stata recuperata? (Evitare i falsi negativi).
- **F-Measure**: Media armonica tra Precision e Recall per avere un unico valore di sintesi.
- **MAP (Mean Average Precision)**: Calcola la precisione media per ogni query, considerando la posizione dei documenti rilevanti nel ranking. È la metrica d'elezione per valutare la qualità dell'ordinamento.

---

## 6. IR Moderna: Dense Retrieval e Embeddings

L'IR classica (Sparse Retrieval) soffre del **Vocabulary Mismatch**: se cerco "felino" e il documento dice "gatto", non ci sarà match. La soluzione è il **Dense Retrieval**.

### Word e Sentence Embeddings
Invece di usare termini discreti, le parole e i documenti vengono mappati in vettori densi di numeri reali (embedding) in uno spazio semantico. In questo spazio, "gatto" e "felino" sono vicini perché appaiono in contesti simili.

### Bi-Encoder vs Cross-Encoder
Per gestire l'efficienza e la precisione, si usano due architetture:
- **Bi-Encoder**: Codifica la query e i documenti separatamente in vettori. Il matching è un semplice prodotto scalare (velocissimo, ideale per milioni di documenti).
- **Cross-Encoder**: Passa query e documento insieme a un modello (come BERT) per analizzare l'interazione parola per parola. È estremamente preciso ma lentissimo (usato solo per il re-ranking dei primi 10-50 risultati).
