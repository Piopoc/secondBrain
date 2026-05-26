---
date: 2026-05-25
source:
  - - raw/VERT_screenrecording-2026-05-25_17-08-41
tags:
  - synthesis
  - statistical-testing
  - neural-networks
  - transformers
  - bert
  - attention
  - text-generation
featured: true
---

# Riepilogo: Advanced IR — Statistical Testing, Neural Models e Architetture Evolute

Sintesi completa della sessione di registrazione VERT, che copre i fondamenti del testing statistico in IR, la classificazione con regressione logistica, i modelli neurali per il language modeling (FFNN, RNN, Encoder-Decoder), l'attenzione e i Transformer, fino a BERT e alle strategie di decoding.

---

## 1. Statistical Testing per la Valutazione in IR

### 1.1 Perché il solo confronto visivo non basta

Confrontando due sistemi di ranking (new vs base) su 50 query:
- **Media**: new ha media più alta di base
- **Box plot**: i baffi delle due distribuzioni si sovrappongono
- **Problema**: la differenza osservata potrebbe essere dovuta a **rumore** del campionamento (osserviamo solo un campione, non l'intera popolazione)

**Conclusione**: Non basta osservare la media più alta né i box plot — serve un test formale di ipotesi per determinare se la differenza è **statisticamente significativa**.

### 1.2 Formulazione del test di ipotesi (t-test appaiato)

- **H₀** ($\mu_{\text{new}} = \mu_{\text{base}}$): I sistemi hanno la stessa performance media
- **H₁** ($\mu_{\text{new}} \neq \mu_{\text{base}}$): I sistemi hanno performance diverse (test a due code)
- **Assunzioni**: Normalità, indipendenza, omoschedasticità (varianza circa uguale)

### 1.3 Perché la distribuzione t di Student e non la Normale?

Nel **Teorema del Limite Centrale (CLT)** si usa la **varianza della popolazione**, che è nota. Nel **t-test** la varianza della popolazione è **ignota** e viene **stimata** dal campione. Questa stima introduce incertezza aggiuntiva, compensata dalla distribuzione **t di Student**, che ha code più pesanti della normale.

I **gradi di libertà** ($df = n - 1$) rappresentano il numero di osservazioni indipendenti meno il numero di parametri stimati (la media). Più $n$ cresce, più la t di Student si avvicina alla normale standard.

### 1.4 Comparazioni Multiple e FWER

Confrontando $k$ sistemi a coppie:
$$\binom{k}{2} = \frac{k(k-1)}{2}$$ Esempio: con 10 sistemi → 45 confronti.

**Family-Wise Error Rate (FWER)**: Probabilità di commettere **almeno un** errore di Tipo I:
$$P(\text{almeno 1 errore}) = 1 - (1 - \alpha)^{\binom{k}{2}}$$

Con $\alpha = 0.05$ e 10 sistemi: $1 - (0.95)^{45} \approx 0.90$ — il 90%!

**Correzione di Bonferroni**: $\alpha_{\text{Bonf}} = \alpha / m$ (conservativa).

### 1.5 ANOVA: One-Way vs Two-Way

| Modello | Componenti | Limitazione |
|---|---|---|
| **One-Way ANOVA** | Solo effetto sistema | La varianza tra topic (molto grande in IR) finisce nell'errore residuo, gonfiandolo e causando **errori di Tipo II** (falsi negativi) |
| **Two-Way ANOVA** | Effetto sistema + effetto topic | Modella entrambe le fonti di varianza, riducendo l'errore residuo |

**Perché la Two-Way è raccomandata in IR**: Le mappe di calore empiriche mostrano che la **varianza tra topic è enormemente maggiore della varianza tra sistemi**. Se non si modella l'effetto topic, tutta questa varianza finisce nell'errore residuo, rendendo difficile rilevare differenze reali tra i sistemi.

$$F = \frac{MS_{\text{System}}}{MS_{\text{Error}}}$$

Se $MS_{\text{Error}}$ diminuisce (perché la varianza dei topic viene ora modellata separatamente), $F$ aumenta → maggiore potenza statistica.

### 1.6 Errori Statistici in IR

- **Tipo I (Falso Positivo)**: Dichiarare un sistema migliore quando non lo è
- **Tipo II (Falso Negativo)**: Non rilevare una differenza reale tra sistemi (più insidioso in IR con campioni piccoli)

---

## 2. Logistic Regression: Classificazione per IR

### 2.1 Classificazione Binaria

La regressione logistica è il modello più semplice per la classificazione in IR:
- **Input**: Vettore di features $(f_1, f_2, ..., f_n)$ scelte manualmente
  - Esempi: numero di parole, conteggio parole positive, presenza di negazioni, TF-IDF
- **Pesi**: Vettore di pesi $(w_1, w_2, ..., w_n)$ — ogni peso indica l'importanza della feature corrispondente
- **Combinazione lineare**: $z = \sum w_i f_i + \text{bias}$
- **Sigmoide**: $\sigma(z) = \frac{1}{1 + e^{-z}}$ — mappa $z$ in una probabilità tra 0 e 1

### 2.2 Training

- **Loss function**: **Cross-Entropy Loss** (negative log likelihood)
  - Se realtà = 1 e modello predice 0.9 → errore basso
  - Se realtà = 1 e modello predice 0.1 → errore alto
- **Gradient Descent / SGD**: Calcola il gradiente della loss rispetto ai pesi e aggiorna i pesi nella direzione che riduce l'errore
  - $\text{peso}_{\text{new}} = \text{peso}_{\text{old}} - \eta \cdot \nabla L$

### 2.3 Generalizzazione a Multi-Classe: Softmax

Per classificazione multi-classe (es. categorizzazione documenti), si sostituisce la sigmoide con la **softmax**:
$$\text{softmax}(y_i) = \frac{e^{y_i}}{\sum_{j=1}^K e^{y_j}}$$

Il resto del meccanismo (features, pesi, cross-entropy, SGD) rimane identico.

---

## 3. Feedforward Neural Networks (FFNN) per Language Modeling

### 3.1 Da Logistic Regression a Reti Neurali

- **Singolo neurone**: $\text{output} = \sigma(Wx + b)$ (somma pesata + attivazione)
- **Rete Feedforward**: Input → Hidden Layer(s) → Output Layer
  - $h = g(W_1 x + b_1)$ (con attivazione non lineare, es. ReLU, sigmoid)
  - $y = \text{softmax}(W_2 h + b_2)$

### 3.2 One-Hot Encoding → Embedding

- **One-hot vector**: Vettore di dimensione $V$ (dimensione vocabolario) con un singolo 1
- **Embedding matrix**: $E \in \mathbb{R}^{V \times d}$ (appresa durante training)
- **Prodotto**: $e_{\text{parola}} = \text{one-hot} \times E$ → vettore denso $d$-dimensionale
  - Da $V$ dimensioni (es. 100.000) si passa a $d = 50\text{-}100$ dimensioni
- **Perdita di interpretabilità**: I vettori densi sono "black magic" — non possiamo ispezionare manualmente cosa rappresenti ogni dimensione

### 3.3 Finestra di Contesto (Context Window)

- **Contesto fisso**: Es. 3 parole precedenti per predire la parola successiva
- **Input layer**: Concatenazione degli embedding delle parole di contesto
  - $x_{\text{input}} = [e_{t-3}, e_{t-2}, e_{t-1}]$ (dimensione $3d$)
- **Output**: Softmax su tutto il vocabolario — probabilità $P(w_t | w_{t-3}, w_{t-2}, w_{t-1})$

### 3.4 Self-Supervision

- **Nessuna etichetta umana**: Il ground truth viene estratto automaticamente dal testo
  - Input = finestra di contesto
  - Target = parola successiva effettiva
- **Sliding window**: Scorrendo il testo, ogni parola diventa target a turno
- **Generazione autoregressiva**: La parola predetta viene reinserita nel contesto per predire la successiva, iterativamente

### 3.5 Training e Backpropagation

- **Forward pass**: Input → Embedding → Hidden Layer → Output → Softmax → Probabilità
- **Loss**: Cross-entropy tra distribuzione predetta e one-hot della parola target
- **Backpropagation**: Propaga l'errore all'indietro attraverso la rete
  - Sensibilità: quanto ogni peso ha contribuito all'errore
  - Aggiornamento: SGD con learning rate per minimizzare la loss
- **Epoche**: L'intero processo viene ripetuto per più passate complete sul corpus

### 3.6 Output del Training

1. **Modello di language modeling**: Predittore di parole funzionante
2. **Matrice di embedding appresa**: Può essere riutilizzata come rappresentazione di parole per altri task IR

---

## 4. Reti Ricorrenti (RNN)

### 4.1 RNN: Gestione delle Sequenze

- **Hidden state**: $h_t = g(U h_{t-1} + W x_t)$
  - $U$: matrice ricorrente (pesi per lo stato precedente)
  - $W$: matrice per l'input corrente
- **Memoria**: Lo stato nascosto funge da contesto cumulativo per l'intera sequenza

### 4.2 Due Problemi Critici delle RNN

1. **Non parallelizzabile**: Il calcolo di $h_t$ dipende da $h_{t-1}$, impedendo l'elaborazione parallela
2. **Vanishing Gradient**: Moltiplicando ripetutamente valori < 1 durante la backpropagation (la matrice $U$ moltiplicata per sé stessa a ogni passo temporale), il gradiente diventa esponenzialmente piccolo → il modello non apprende dipendenze a lungo raggio
   > *"Se continui a moltiplicare numeri minori di 1 diventano sempre più piccoli provocando una lenta convergenza o blocco dell'apprendimento"*

### 4.3 Soluzioni al Vanishing Gradient

- utilizzare un valore soglia da non superare -> stabilizzazione apprendimento
- utilizzare funzioni di attivazioni specifiche come ReLu (gradiente non nullo per valori positivi) e non sigmoid o tanh

### 4.4 Teacher Forcing

Durante il training sequenziale:
- Se la rete genera una parola sbagliata (es. "Monday" invece di "Tuesday")
- **Non** si usa l'output errato come input per il passo successivo
- Si **forza** l'input corretto (si usa la parola giusta dal dataset di training)
- Questo accelera e stabilizza l'apprendimento

---

## 5. Architettura Encoder-Decoder e Attenzione

### 5.1 Encoder-Decoder

- **Encoder**: RNN che processa l'intera sequenza di input e produce un **context vector** (ultimo hidden state)
- **Decoder**: RNN che riceve il context vector come input iniziale e genera la sequenza di output
- **Bottleneck**: Il context vector è di dimensione fissa → impossibile comprimere frasi lunghe in un singolo vettore senza perdere informazioni critiche

### 5.2 Meccanismo di Attenzione

**Soluzione al bottleneck**: Il decoder ha accesso a **tutti** gli hidden state dell'encoder, non solo all'ultimo.

Processo passo-passo:
1. **Score**: Calcola similarità (dot product) tra lo stato corrente del decoder e ogni hidden state dell'encoder
   - Stessa logica del calcolo di similarità nei motori di ricerca
2. **Attention Weights**: Applica softmax agli score → pesi che sommano a 1
3. **Dynamic Context Vector**: Somma pesata di tutti gli hidden state dell'encoder
   - Contesto **dinamico**: cambia a ogni passo del decoder
   - Se il decoder deve tradurre il soggetto, l'attenzione si concentra sulla parola del soggetto nell'input
   - Al passo successivo (es. verbo), l'attenzione si sposta sulla parola del verbo

**Parallelismo con IR**: Il calcolo dei pesi di attenzione equivale a un task di information retrieval — *"quanto è simile questo token del decoder a ogni token dell'encoder?"*

### 5.3 Self-Attention (precursore nei Transformer)

- Ogni token della sequenza interagisce con **tutti gli altri token** della stessa sequenza
- **Query, Key, Value**: Lo stesso token viene proiettato in tre spazi diversi tramite tre matrici apprese ($W_Q$, $W_K$, $W_V$)
  - **Query (Q)**: valore che sto cercando
  - **Key (K)**: la label che rappresenta il token per il matching
  - **Value (V)**: valore effettivo da estrarre
- **Scaled Dot-Product Attention**:
  $$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

---

## 6. Transformer: La Rivoluzione

### 6.1 Self-Attention nei Transformer

**Differenza dall'attenzione classica**: 
- Attenzione classica: decoder interroga encoder (cross-attention)
- Self-attention: ogni token interroga tutti gli altri token della **stessa** sequenza

**Query-Key-Value in dettaglio**:
- **Query**: Rappresenta il token su cui ci si concentra
- **Key**: Rappresenta il token valutato dalla query
- **Value**: È il contenuto effettivo — se query e key hanno alto match, il valore contribuirà significativamente alla rappresentazione finale

### 6.2 Perché Self-Attention è Superiore alle RNN

| Caratteristica | RNN | Transformer (Self-Attention) |
|---|---|---|
| Complessità sequenziale | $O(n)$ (deve processare token uno alla volta) | $O(1)$ (tutti i token in parallelo) |
| Dipendenze a lungo raggio | Peggiora con distanza (vanishing gradient) | Sempre $O(1)$ — qualsiasi token comunica direttamente con qualsiasi altro |
| Parallelizzazione | Impossibile | **Completa** — tutti i token processati simultaneamente |

### 6.3 Multi-Head Attention

- **Più teste di attenzione** operano in parallelo, ciascuna con le proprie matrici $W_Q$, $W_K$, $W_V$
- Ogni testa cattura relazioni diverse:
  - Una testa per relazioni sintattiche (es. soggetto-verbo)
  - Una testa per dipendenze a lunga distanza
  - Una testa per entità e relazioni semantiche
- I risultati di tutte le teste vengono concatenati e proiettati tramite un'ulteriore matrice $W_O$

### 6.4 Componenti Chiave del Transformer

1. **Residual Connections** (Residual Stream): $x_{\text{new}} = x_{\text{old}} + \text{Attention}(x_{\text{old}})$
   - Permette all'informazione di fluire direttamente attraverso i layer
   - Previene la scomparsa del gradiente
   - Stabilizza l'addestramento di reti profonde
2. **Layer Normalization**: Normalizza le attivazioni per mantenere valori in range stabile
3. **Positional Embeddings**: Poiché self-attention è **invarante alla posizione** (scambia due token e ottieni lo stesso risultato), si aggiungono vettori posizionali
   - Nel paper originale: funzioni seno/coseno a diverse frequenze
   - Ogni posizione riceve una **firma unica**
   - *"L'hanno provata e ha funzionato — la giustificazione formale era empirica"*

### 6.5 Mascheramento Causale (Decoder)

Nel **decoder** (modello causale/autoregressivo):
- I token non possono "guardare avanti" ai token futuri
- La matrice dei pesi di attenzione è **mascherata**: i pesi per i token futuri sono impostati a $-\infty$ prima della softmax, diventando zero
- Questo garantisce che la predizione al tempo $t$ dipenda solo dai token passati ($< t$)

---

## 7. BERT: Pre-training e Fine-Tuning

### 7.1 Architettura Encoder-Only (BERT)

- **Bidirezionale**: A differenza del decoder causale, BERT guarda sia a sinistra che a destra
- **Task principale**: **Masked Language Modeling (MLM)**
  - 15% dei token vengono mascherati (sostituiti con `[MASK]`)
  - Di questi 15%: 80% → `[MASK]`, 10% → parola casuale, 10% → invariato
  - Il modello deve predire i token originali
  - *"Alcune parole non sono state modificate e altre sì — il modello deve capire quali"*

### 7.2 Next Sentence Prediction (NSP)

- **Task secondario**: Dopo MLM, si sostituisce la testa e si aggiunge NSP
- **Input**: Due frasi separate dal token `[SEP]`
- **Classificazione binaria**: La seconda frase è consecutiva alla prima? (sì/no)
- **Token `[CLS]`**: Inserito all'inizio della sequenza, la sua rappresentazione finale viene usata per la classificazione (con una sigmoide)

### 7.3 Fine-Tuning

- **Pre-training**: Costoso, su enormi quantità di dati non etichettati (MLM + NSP)
- **Fine-tuning**: Veloce, su singola GPU
  - Si rimuovono le teste pre-training (MLM, NSP)
  - Si aggiunge una testa specifica per il task (classificazione, QA, etichettatura)
  - Si addestra su dataset etichettato di dimensioni contenute
  - Solo **minimi aggiustamenti** ai pesi pre-addestrati

### 7.4 Architetture Transformer: Le Tre Varianti

| Tipo | Modello | Caratteristica | Task |
|---|---|---|---|
| **Encoder-only** | BERT | Bidirezionale, guarda tutto | Comprensione, classificazione, QA |
| **Decoder-only** | GPT | Causale, guarda solo passato | Generazione autoregressiva |
| **Encoder-Decoder** | T5 | Unisce i due | Seq2seq (traduzione, riassunto) |

---

## 8. Strategie di Decoding

### 8.1 Greedy Decoding
- Sceglie sempre il token più probabile
- **Problema**: Testo ripetitivo e prevedibile ("troppo ovvio")

### 8.2 Temperature Sampling
- Scala i logit prima della softmax: $p_i = \frac{e^{z_i / T}}{\sum e^{z_j / T}}$
  - **T bassa** (es. 0.2): Distribuzione più sharp, quasi greedy
  - **T alta** (es. 1.5): Distribuzione più uniforme, più creativa/random

### 8.3 Top-k Sampling
- Considera solo i $k$ token con probabilità più alta
- **Problema**: Con $k$ fisso, a volte si include troppo rumore

### 8.4 Top-p (Nucleus) Sampling
- Considera il sottoinsieme minimo di token la cui probabilità cumulativa supera $p$

### 8.5 Beam Search
- Mantiene attivi **più percorsi** di generazione in parallelo (beam width)
- Ogni passo, per ogni percorso, si espande considerando i token più probabili
- Si mantengono i $k$ percorsi globalmente più probabili
- Alla fine, si sceglie la sequenza con probabilità complessiva più alta
- Esempio: "The green witch" vs "The green witch" → beam search esplora entrambe le ramificazioni

---

## 9. Collegamenti e Parallelismi

### Self-Attention ↔ Rocchio Relevance Feedback
- **Rocchio**: Muove il vettore query verso il centro dei documenti rilevanti e lontano dai non rilevanti
- **Self-Attention**: Sposta l'embedding di un token verso i token che l'attenzione indica come rilevanti per il contesto
- Stessa idea di base: **aggiustare rappresentazioni basandosi su ciò che è rilevante**

### Attenzione ↔ Ricerca per Similarità in IR
- Il calcolo degli score di attenzione (dot product) è **identico** al calcolo di similarità nei motori di ricerca
- *"Nell'attenzione, ogni passo del decoder fa essenzialmente una query di retrieval su tutti gli hidden state dell'encoder"*
