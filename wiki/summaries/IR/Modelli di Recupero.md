# IR - Modelli di Recupero
 
I modelli di recupero definiscono la funzione di matching $R(q, d)$ che assegna un punteggio di rilevanza a un documento $d$ data una query $q$.
 
## 0. Pipeline di Indicizzazione e Preprocessing
Prima che i modelli di recupero possano calcolare la rilevanza, i documenti devono essere processati e organizzati in una struttura efficiente.
 
### Apache Lucene
**[[Apache-Lucene]]** è la libreria open-source standard (in Java) per l'indicizzazione e la ricerca. È il motore alla base di sistemi industriali come **[[Elasticsearch]]** e **[[Apache Solr]]**.
 
### La Pipeline di Analisi (Analyzer)
Un documento grezzo non viene indicizzato così com'è, ma passa attraverso un **Analyzer** che esegue una serie di trasformazioni:
1. **[[Tokenization]]**: Divisione del testo in singoli termini (token) tramite un `Tokenizer`.
2. **Case Folding**: Conversione di tutti i termini in minuscolo (`LowerCaseFilter`) per rendere la ricerca case-insensitive.
3. **Rimozione [[Stopwords]]**: Eliminazione di parole comuni e prive di valore semantico (es. "il", "di", "lo") tramite un `StopFilter`.
4. **[[Stemming]]**: Riduzione delle parole alla loro radice linguistica (es. "programmazione" $\rightarrow$ "program") per gestire le flessioni. Un esempio comune è il `PorterStemFilter`.
 
**Regola Fondamentale**: L'analyzer utilizzato durante l'**indicizzazione** dei documenti deve essere identico a quello utilizzato durante l'**analisi della query**. Se i termini della query non vengono processati nello stesso modo di quelli dell'indice, il matching fallirà.
 
### L'Indice Invertito (Inverted Index)
Il risultato finale della pipeline è l'**[[Inverted Index]]**. Invece di mappare `Documento` $\rightarrow$ `Termini`, l'indice invertito mappa `Termine` $\rightarrow$ `Lista di Documenti` che lo contengono. Questa struttura è ciò che permette ai modelli di recupero di operare in tempi millisecondi anche su milioni di documenti.
 
---
 
## 1. [[Boolean-Model]] (Bool. Mod.)
È il modello più semplice, basato sulla teoria degli insiemi e l'algebra di Boole.

- **Logica**: La query è un'espressione booleana (AND, OR, NOT). Il risultato è un insieme di documenti che soddisfano la condizione (non c'è ranking).
- **Struttura Dati**: Matrice invertita (Termini $\times$ Documenti) con valori binari $\{0, 1\}$.
- **Funzione di Matching**:
  $$R(q, d) = \begin{cases} 1, & \text{se l'espressione è vera} \\ 0, & \text{altrimenti} \end{cases}$$
- **Vantaggi**: Risultati prevedibili, processing efficiente.
- **Svantaggi**: L'efficacia dipende totalmente dall'utente (che deve scrivere la query perfetta), non considera la frequenza dei termini, query complesse difficili da gestire.

---

## 2. [[Vector-Space-Model]] (VSM)
I documenti e le query sono rappresentati come vettori in uno spazio $V$-dimensionale.

### [[Cosine-Similarity]]
La rilevanza è misurata come il coseno dell'angolo $\theta$ tra il vettore query $\vec{q}$ e il vettore documento $\vec{d}$:
$$R(q, d) = \cos(\theta(\vec{q}, \vec{d})) = \frac{\vec{q} \cdot \vec{d}}{\|\vec{q}\| \cdot \|\vec{d}\|} = \frac{\sum_{i=1}^V q_i d_{i,k}}{\sqrt{\sum_{i=1}^V q_i^2} \cdot \sqrt{\sum_{i=1}^V d_{i,k}^2}}$$

### Pesatura dei Termini (Weighting)
Non tutti i termini sono ugualmente utili. Si utilizza lo schema **[[TF-IDF]]**:

1. **TF (Term Frequency)**: Misura l'importanza del termine nel singolo documento.
($tf_{i,k}$: frequenza del termine $i$ nel documento $k$)
($\text{denominatore}$: somma delle frequenze di tutti i termini nel documento $k$)
   - *Relative TF*: $tf_{i,k} = \frac{f_{i,k}}{\sum_{j=1}^N f_{j,k}}$
   - *Log-scaled TF*: $\begin{cases} 1 + \log_2(f_{i,k}), & \text{se } f_{i,k} > 0 \\ 0, & \text{altrimenti} \end{cases}$
1. **IDF (Inverse Document Frequency)**: Misura il potere risolutivo del termine sull'intero corpus.
   $$idf_i = \log_2 \frac{N}{n_i}$$
   Dove $N$ è il numero totale di documenti e $n_i$ il numero di documenti che contengono il termine $i$.
2. **TF-IDF**: $w_{ik} = tf_{ik} \cdot idf_i$

### Leggi Fondamentali
- **[[Zipf-Law]]**: La frequenza di un termine è inversamente proporzionale al suo rango ($Pr \sim \frac{C}{r^\alpha}$).
- **Principio del Minimo Sforzo**: Le parole più frequenti tendono a essere brevi (funzionali).

---

## 3. Relevance Feedback (RF)
Tecnica per migliorare la query basandosi sui risultati di una prima ricerca.

### [[Rocchio-Algorithm]]
L'obiettivo è spostare il vettore query $\vec{q}$ verso il centro dei documenti rilevanti e lontano da quelli non rilevanti.
$$\vec{q}'_i = \alpha \vec{q}_i + \beta \frac{1}{|\text{Rel}|} \sum_{d \in \text{Rel}} \vec{d}_{i,k} - \gamma \frac{1}{|\text{NotRel}|} \sum_{d \in \text{NotRel}} \vec{d}_{i,k}$$
- $\alpha, \beta, \gamma$ sono pesi di importanza.
- **Pseudo-Relevance Feedback**: Il sistema assume che i primi $K$ documenti del ranking siano tutti rilevanti e aggiorna la query automaticamente.
- **Limite**: Rischio di *query drifting* (la query si sposta troppo lontano dall'intento originale).

---

## 4. Modelli Probabilistici
L'IR è visto come un problema di classificazione Bayesiana: data una query, qual è la probabilità che un documento sia rilevante?

### [[Binary-Independence-Model]] (BIM)
Il BIM mira a stimare la probabilità che un documento $d$ sia rilevante $R$ data una query $q$.

**Passaggi per la derivazione:**
1. **Teorema di Bayes**: Vogliamo calcolare $P(R|d, q)$.
   $$P(R|d, q) = \frac{P(d|R, q) P(R|q)}{P(d|q)}$$
2. **Odds Ratio**: Per confrontare due documenti, analizziamo il rapporto tra la probabilità di essere rilevante e non rilevante ($\overline{R}$):
   $$\frac{P(R|d, q)}{P(\overline{R}|d, q)} = \frac{P(d|R, q)}{P(d|\overline{R}, q)} \cdot \frac{P(R|q)}{P(\overline{R}|q)}$$
   Il secondo termine è costante per tutti i documenti, quindi ci concentriamo sul rapporto delle verosimiglianze $\frac{P(d|R, q)}{P(d|\overline{R}, q)}$.
3. **Assunzioni BIM**:
   - **Binarizzazione**: Un termine $i$ è presente ($x_i=1$) o assente ($x_i=0$).
   - **Indipendenza**: La presenza di un termine è indipendente dagli altri, data la rilevanza.
   $$P(d|R, q) = \prod_{i \in q} P(x_i | R)$$
4. **Formula Finale**: Definendo $p_i = P(x_i=1 | R)$ e $s_i = P(x_i=1 | \overline{R})$, e applicando il logaritmo per trasformare il prodotto in somma:
   $$R(q, d) \sim \sum_{i \in q} \log_2 \frac{P(x_i | R)}{P(x_i | \overline{R})} = \sum_{i \in q} \log_2 \frac{p_i^{x_i}(1-p_i)^{1-x_i}}{s_i^{x_i}(1-s_i)^{1-x_i}}$$
   Semplificando per i termini presenti nel documento ($x_i=1$):
   $$R(q, d) \sim \sum_{i \in Q \cap D} \log_2 \frac{p_i(1-s_i)}{s_i(1-p_i)}$$

### [[BM25]] (Best Match 25)
Il BM25 è un'evoluzione del BIM che corregge due limiti principali: l'assenza di TF e l'effetto della lunghezza del documento.

**Passaggi concettuali per arrivare alla formula:**
1. **Oltre il Binario (TF)**: Il BIM considera solo se un termine è presente. BM25 introduce la frequenza del termine $f_i$.
2. **Saturazione della TF**: Aumentare la frequenza di un termine aumenta la rilevanza, ma con rendimenti decrescenti. Passare da 0 a 1 occorrenza è fondamentale; passare da 100 a 101 è irrilevante.
   - Si introduce una funzione di saturazione: $\frac{f_i}{f_i + k_1}$.
3. **Normalizzazione della Lunghezza**: Documenti più lunghi tendono ad avere TF più alte semplicemente perché contengono più parole. Per evitare che i documenti lunghi siano favoriti ingiustamente, si normalizza la TF rispetto alla lunghezza media dei documenti ($\text{avgdl}$).
   - Il parametro $b \in [0, 1]$ controlla quanto pesare questa normalizzazione.
4. **Sintesi**: Combinando il peso probabilistico del BIM (IDF) con la TF saturata e normalizzata, si ottiene:
   $$R(q, d) = \sum_{i \in Q \cap D} \text{IDF}_i \cdot \frac{f_i \cdot (k_1 + 1)}{f_i + k_1 \cdot (1 - b + b \frac{|d|}{\text{avgdl}})}$$
   Dove $\text{IDF}_i = \log \frac{N - n_i + 0.5}{n_i + 0.5}$.

---

## 5. [[Language-Models-IR]] (LM)
L'IR è approcciata come un problema di modellazione linguistica: ogni documento è visto come un modello generativo di testo (una distribuzione di probabilità su sequenze di parole).

### L'Intuizione: Query Likelihood Model (QLM)
L'idea centrale è: **"Qual è la probabilità che la query $q$ sia stata generata dal modello linguistico del documento $d$?"**
Invece di calcolare $P(R|d, q)$ (come nel BIM), calcoliamo la verosimiglianza della query dato il documento:
$$R(q, d) = P(q|d) = \prod_{i=1}^{|q|} P(w_i|d)$$
Dove $w_i$ sono i termini della query. I documenti che "genererebbero" più facilmente la query sono considerati i più rilevanti.

### Modellazione e Stima
- **Unigram Model**: Assume che ogni parola sia generata indipendentemente dalle altre (bag-of-words).
- **Maximum Likelihood Estimator (MLE)**: La stima più semplice della probabilità di un termine $w_i$ in un documento $d$:
  $$\hat{P}(w_i | \Theta_d) = \frac{f_{w_i, d}}{|d|}$$
  Dove $f_{w_i, d}$ è la frequenza del termine e $|d|$ la lunghezza del documento.

### Il Problema dello Zero e lo Smoothing
L'MLE soffre del **problema della frequenza zero**: se un termine della query non appare nel documento, $P(w_i|d) = 0$, rendendo l'intero prodotto $P(q|d) = 0$, indipendentemente dagli altri termini. Per risolvere questo, si usa lo **Smoothing** (livellamento), che redistribuisce parte della massa di probabilità dai termini presenti a quelli assenti.

1. **[[Laplace-Smoothing]] (Additive)**: Aggiunge un valore costante $\delta$ a ogni conteggio.
   $$P(w_i | \Theta_d) = \frac{f_{w_i, d} + \delta}{|d| + \delta |V|}$$ (dove $|V|$ è la dimensione del vocabolario).
2. **[[Jelinek-Mercer-Smoothing]]**: Interpolazione lineare tra il modello del documento e il modello della collezione (background).
   $$P(w_i | \hat{\Theta}_d) = (1-\lambda) \frac{f_{w_i, d}}{|d|} + \lambda \frac{f_{w_i, C}}{|C|}$$
   $\lambda$ controlla il bilanciamento tra l'evidenza locale (doc) e globale (collezione).
3. **[[Dirichlet-Smoothing]]**: Assume che il documento sia un campione di una distribuzione di Dirichlet. Si aggiungono "parole virtuali" basate sulla collezione.
   $$P(w_i | \hat{\Theta}_d) = \frac{f_{w_i, d} + \mu \frac{f_{w_i, C}}{|C|}}{|d| + \mu}$$
   Dove $\mu$ è un parametro di smoothing.

### Altri Approcci LM
- **Divergenza di Kullback-Leibler (KL)**: Invece della likelihood, si misura la "distanza" tra la distribuzione di probabilità della query $P(q)$ e quella del documento $P(d)$.
- **Nota Teorica**: A differenza dei modelli probabilistici classici (BIM/BM25) che sono *discriminativi* (distinguono tra rilevanti e non), i modelli LM sono *generativi* (modellano come i documenti sono prodotti).
