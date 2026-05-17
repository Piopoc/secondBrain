# IR - Tipologie di Esercizi Numerici

Questo documento cataloga le principali tipologie di esercizi numerici che possono essere riscontrati in un esame di Information Retrieval (IR), suddivisi per area tematica, con un esempio svolto per ogni categoria.

---

## 1. Vector Space Model (VSM) e TF-IDF
Questi esercizi testano la capacità di rappresentare documenti e query come vettori e di misurarne la similarità.

### Tipologie di Task:
- **Calcolo TF (Term Frequency)**: Calcolare la TF relativa o log-scaled.
- **Calcolo IDF (Inverse Document Frequency)**: Calcolare l'IDF dato $N$ e $n_i$.
- **Costruzione della Matrice TF-IDF**: Calcolare i pesi $w_{ik}$.
- **Cosine Similarity**: Calcolare il coseno tra $\vec{q}$ e $\vec{d}$.

### 📝 Esercizio Svolto: Cosine Similarity
**Testo**: Consideriamo due documenti e una query:
- $D_1$: "gatto cane"
- $D_2$: "gatto topo"
- $Q$: "cane topo"

Calcolare la similarità tra la query e i documenti usando TF binaria e $\text{IDF} = \log_2(N/n_i)$.

**Svolgimento**:
1. **Vocabolario**: {gatto, cane, topo} $\rightarrow N=2$.
2. **IDF**:
   - $\text{IDF}_{\text{gatto}} = \log_2(2/2) = 0$
   - $\text{IDF}_{\text{cane}} = \log_2(2/1) = 1$
   - $\text{IDF}_{\text{topo}} = \log_2(2/1) = 1$
3. **Vettori TF-IDF**:
   - $\vec{D_1} = [1\cdot 0, 1\cdot 1, 0\cdot 1] = [0, 1, 0]$
   - $\vec{D_2} = [1\cdot 0, 0\cdot 1, 1\cdot 1] = [0, 0, 1]$
   - $\vec{Q} = [0\cdot 0, 1\cdot 1, 1\cdot 1] = [0, 1, 1]$
4. **Cosine Similarity**:
   - $R(Q, D_1) = \frac{0\cdot 0 + 1\cdot 1 + 0\cdot 1}{\sqrt{0^2+1^2+0^2} \cdot \sqrt{0^2+1^2+1^2}} = \frac{1}{1 \cdot \sqrt{2}} \approx 0.707$
   - $R(Q, D_2) = \frac{0\cdot 0 + 0\cdot 1 + 1\cdot 1}{\sqrt{0^2+1^2+0^2} \cdot \sqrt{0^2+0^2+1^2}} = \frac{1}{1 \cdot \sqrt{2}} \approx 0.707$

---

## 2. Modelli Probabilistici (BIM e BM25)
Esercizi focalizzati sulla stima della probabilità di rilevanza.

### Tipologie di Task:
- **BIM Weight**: Calcolare il peso $\log_2 \frac{p_i(1-s_i)}{s_i(1-p_i)}$.
- **Punteggio BM25**: Calcolare il punteggio applicando saturazione TF e normalizzazione lunghezza.

### 📝 Esercizio Svolto: Punteggio BM25
**Testo**: Calcolare il punteggio BM25 per il termine "IR" in un documento $d$ con:
- $f_{IR, d} = 2$ (frequenza del termine nel doc)
- $|d| = 5$ (lunghezza doc), $\text{avgdl} = 4$ (lunghezza media corpus)
- $k_1 = 1.2$, $b = 0.75$, $\text{IDF}_{IR} = 2.1$

**Svolgimento**:
1. **Formula**: $R(q, d) = \text{IDF} \cdot \frac{f \cdot (k_1 + 1)}{f + k_1 \cdot (1 - b + b \frac{|d|}{\text{avgdl}})}$
2. **Sostituzione**:
   - Denominatore TF: $2 + 1.2 \cdot (1 - 0.75 + 0.75 \cdot \frac{5}{4}) = 2 + 1.2 \cdot (0.25 + 0.9375) = 2 + 1.2 \cdot 1.1875 = 2 + 1.425 = 3.425$
   - Numeratore TF: $2 \cdot (1.2 + 1) = 2 \cdot 2.2 = 4.4$
3. **Risultato**: $R(q, d) = 2.1 \cdot \frac{4.4}{3.425} \approx 2.1 \cdot 1.285 \approx 2.698$

---

## 3. Language Models (LM)
Esercizi sulla modellazione generativa del testo.

### Tipologie di Task:
- **Stima MLE**: Calcolare $\hat{P}(w_i | \Theta) = \frac{f_i}{|d|}$.
- **Smoothing**: Applicare Laplace, Jelinek-Mercer o Dirichlet.
- **Query Likelihood**: Calcolare $P(q|d) = \prod P(w_i|d)$.

### 📝 Esercizio Svolto: Jelinek-Mercer Smoothing
**Testo**: Un documento $d$ contiene "ciao mondo". La query è "ciao".
- $f_{\text{ciao}, d} = 1, |d| = 2$
- Probabilità del termine nella collezione: $P(\text{ciao} | C) = 0.01$
- Parametro di interpolazione $\lambda = 0.4$

Calcolare la probabilità smooth $P(\text{ciao} | \hat{\Theta}_d)$.

**Svolgimento**:
1. **MLE Locale**: $P(\text{ciao} | d) = \frac{1}{2} = 0.5$
2. **Formula Jelinek-Mercer**: $P(w_i | \hat{\Theta}_d) = (1-\lambda) P(w_i | d) + \lambda P(w_i | C)$
3. **Sostituzione**: $P(\text{ciao} | \hat{\Theta}_d) = (1 - 0.4) \cdot 0.5 + 0.4 \cdot 0.01 = 0.6 \cdot 0.5 + 0.004 = 0.3 + 0.004 = 0.304$

---

## 4. Valutazione del Sistema (Evaluation)
Esercizi di analisi delle performance basati su un ground truth.

### Tipologie di Task:
- **Precision e Recall**: Calcolare P e R a un cutoff $K$.
- **F-Measure**: Media armonica tra P e R.
- **Average Precision (AP) e MAP**: Media delle precisioni nei punti di rilevanza.
- **NDCG**: Calcolare il gain scontato e normalizzarlo.

### 📝 Esercizio Svolto: Precision, Recall e AP
**Testo**: Insieme documenti rilevanti $Rel = \{1, 3, 5\}$.
Risultati restituiti dal sistema: $[1, 2, 3, 4, 6]$.
Calcolare Precision@5, Recall@5 e Average Precision (AP).

**Svolgimento**:
1. **Precision@5**: $\frac{\text{Rilevanti in primi 5}}{5} = \frac{|\{1, 3\}|}{5} = \frac{2}{5} = 0.4$
2. **Recall@5**: $\frac{\text{Rilevanti in primi 5}}{\text{Totale Rilevanti}} = \frac{2}{3} \approx 0.66$
3. **Average Precision (AP)**:
   - Posizione 1: Rilevante $\rightarrow P@1 = 1/1 = 1.0$
   - Posizione 2: Non rilevante
   - Posizione 3: Rilevante $\rightarrow P@3 = 2/3 \approx 0.66$
   - Posizione 4: Non rilevante
   - Posizione 5: Non rilevante
   - $AP = \frac{1.0 + 0.66}{3} = \frac{1.66}{3} \approx 0.55$

---

## 5. Indicizzazione e Compressione
Esercizi sull'efficienza dello storage dell'indice invertito.

### Tipologie di Task:
- **Dimensione Indice**: Stimare lo spazio occupato.
- **Delta Encoding**: Trasformare ID in gap.
- **Codifica Gamma ($\gamma$)**: Convertire un intero in codice Gamma.

### 📝 Esercizio Svolto: Codifica Gamma ($\gamma$)
**Testo**: Convertire il numero intero $5$ in codice Gamma.

**Svolgimento**:
1. **Rappresentazione Binaria**: $5_{10} = 101_2$
2. **Lunghezza**: $L = 3$ bit.
3. **Calcolo Prefisso (Lunghezza-1)**: $L-1 = 2$. In binario: $10_2$.
   - Il prefisso è composto da $L-1$ zeri seguiti da un $1$.
   - Per $L-1=2 \rightarrow 001$
4. **Calcolo Offset**: Sono gli ultimi $L-1$ bit del numero originale.
   - Da $101_2$, l'offset è $01$.
5. **Risultato Finale**: $\text{Prefisso} + \text{Offset} = 00101$

---

## 6. Modello Booleano
Esercizi di logica degli insiemi.

### Tipologie di Task:
- **Risoluzione Query Booleane**: Intersezioni e unioni di posting list.
- **Calcolo Cardinalità**: Stima del numero di documenti risultati.

### 📝 Esercizio Svolto: Operazioni su Posting List
**Testo**: Date le seguenti posting list:
- $L_A = [1, 3, 5, 8]$
- $L_B = [2, 3, 8, 10]$
Calcolare i risultati per:
1. `A AND B`
2. `A OR B`

**Svolgimento**:
1. **A AND B (Intersezione)**: Si cercano gli elementi comuni.
   - $L_A \cap L_B = [3, 8]$
2. **A OR B (Unione)**: Si uniscono gli elementi eliminando i duplicati e mantenendo l'ordine.
   - $L_A \cup L_B = [1, 2, 3, 5, 8, 10]$
