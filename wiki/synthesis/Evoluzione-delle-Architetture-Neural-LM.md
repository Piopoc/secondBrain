---
date: 2026-05-16
source:
  - - raw/12/
tags:
  - synthesis
  - neural-networks
  - deep-learning
  - nlp
  - evolution
featured: true
---

# L'Evoluzione delle Architetture per il Language Modeling: Dalla Regressione ai Transformer

Questo documento rappresenta la sintesi completa dell'evoluzione dei modelli neurali applicati al linguaggio naturale. L'obiettivo del Language Modeling è prevedere la distribuzione di probabilità di un token dato un contesto precedente: $P(w_{t+1} | w_1, \dots, w_t)$.

## 1. Le Fondamenta: Classificazione Lineare e FFNN

Il percorso inizia con la **Regressione Logistica**, l'approccio più semplice per la classificazione binaria. Utilizza la funzione Sigmoide $\sigma(wx) = \frac{1}{1 + \exp(-wx)}$ per mappare una combinazione lineare di feature in una probabilità tra 0 e 1. Il concetto chiave è il *logit* ($\ln \frac{p}{1-p}$), che rappresenta l'input della sigmoide. Per l'addestramento si utilizza la Cross-entropy Loss, ottimizzata tramite lo Stochastic Gradient Descent (SGD).

L'estensione a più classi è la **Regressione Logistica Multinomiale**, che sostituisce la sigmoide con la funzione Softmax:
$$\text{softmax}(y_i) = \frac{\exp y_i}{\sum_{j=1}^K \exp y_j}$$
In questo contesto, i pesi del modello possono essere interpretati come "prototipi" di ogni classe.

Le **Feedforward Neural Networks (FFNN)** evolvono questo concetto aggiungendo strati nascosti e funzioni di attivazione non lineari. Un'unità neurale calcola una somma pesata degli input e applica una funzione $\sigma$ (soglia) per produrre l'output. Nei primi modelli di linguaggio neurali, l'input era una finestra fissa di parole (es. 3 parole), rappresentate tramite One-hot Encoding e proiettate in vettori densi chiamati Embedding. Il limite principale era l'incapacità di gestire contesti più ampi della finestra fissata.

## 2. La Gestione delle Sequenze: RNN e LSTM

Per superare il limite della finestra fissa, nascono le **Recurrent Neural Networks (RNN)**. A differenza delle FFNN, le RNN processano le sequenze un elemento alla volta, mantenendo un **Hidden State** ($h_t$) che funge da memoria.
Lo stato corrente è calcolato come: $h_t = g(U h_{t-1} + W x_t)$, dove $g$ è una funzione di attivazione (tanh, ReLU).

Nonostante l'intuizione, le RNN presentano due problemi critici:
1. **Sequentialità**: Il calcolo di $h_t$ dipende da $h_{t-1}$, impedendo la parallelizzazione dell'addestramento.
2. **Vanishing Gradient Problem**: Durante la backpropagation, i gradienti vengono moltiplicati ripetutamente per i pesi. Se i pesi sono piccoli, il gradiente svanisce, rendendo impossibile l'apprendimento di dipendenze a lungo raggio.

Le **LSTM (Long Short-Term Memory)** risolvono questo problema introducendo una gestione esplicita del contesto tramite "gate". Le LSTM possono decidere attivamente quali informazioni rimuovere dal contesto (Forget Gate) e quali nuove informazioni aggiungere per decisioni future, stabilizzando il flusso del gradiente.

## 3. Il Superamento del Bottleneck: Encoder-Decoder e Attention

Per compiti di traduzione (seq2seq), è stata introdotta l'architettura **Encoder-Decoder**. L'Encoder comprime l'intera sequenza di input in un unico vettore di dimensione fissa chiamato **Context Vector**. Il Decoder poi espande questo vettore per generare la sequenza di output.

Tuttavia, il Context Vector diventa un **collo di bottiglia (bottleneck)**: è matematicamente impossibile comprimere tutto il significato di una frase molto lunga in un unico vettore senza perdere informazioni critiche.

La soluzione è l'**Attention Mechanism**. Invece di un unico vettore statico, l'attenzione permette al decoder di "interrogare" tutti gli stati nascosti dell'encoder a ogni passo della generazione. 
Il processo avviene in tre step:
1. **Score**: Si calcola la similarità tra lo stato del decoder e ogni stato dell'encoder (es. tramite Dot-product Attention: $h^d \cdot h^e$).
2. **Weights**: I punteggi vengono normalizzati con una Softmax per ottenere dei pesi $\alpha$.
3. **Sum**: Si crea un contesto dinamico come somma pesata degli stati dell'encoder.

## 4. La Rivoluzione dei Transformer

Il **Transformer** elimina completamente la ricorrenza, basandosi esclusivamente sull'attenzione. L'innovazione centrale è la **Self-Attention**, che permette a ogni token di una sequenza di interagire con tutti gli altri simultaneamente, indipendentemente dalla distanza.

Il meccanismo si basa su tre ruoli per ogni token:
- **Query (Q)**: Ciò che il token sta cercando.
- **Key (K)**: Ciò che il token offre.
- **Value (V)**: L'informazione effettiva da estrarre.
L'output è $\text{Attention}(Q, K, V) = \text{softmax}(\frac{QK^T}{\sqrt{d_k}})V$.

L'architettura introduce inoltre:
- **Multi-Head Attention**: Più "teste" di attenzione che operano in parallelo per catturare diverse relazioni (es. una testa per la sintassi, una per la semantica).
- **Residual Connections**: Connessioni che saltano i layer per evitare la scomparsa del gradiente.
- **Layer Normalization**: Stabilizzazione delle attivazioni per velocizzare la convergenza.
- **Positional Embeddings**: Poiché non c'è più ricorrenza, l'ordine delle parole viene aggiunto esplicitamente tramite vettori di posizione.

## 5. Modelli Specializzati: BERT, GPT e T5

L'architettura Transformer si è poi specializzata in tre direzioni:

1. **Encoder-only (es. BERT)**: Modelli bidirezionali che guardano l'intera frase. Vengono addestrati con il **Masked Language Modeling (MLM)** (predire parole mascherate in un compito di "riempimento spazi" o Cloze Task) e il **Next Sentence Prediction (NSP)**. Producono **Contextual Embeddings**, dove il vettore di una parola cambia in base al contesto. Usano il token `[CLS]` per rappresentare l'intera sequenza in compiti di classificazione.

2. **Decoder-only (es. GPT)**: Modelli causali che guardano solo al passato. Sono ottimizzati per l'**Autoregressive Generation**, predicendo un token alla volta.

3. **Encoder-Decoder (es. T5)**: Modelli che uniscono i due mondi. Il T5 (Text-to-Text Transfer Transformer) adotta un paradigma unificato dove ogni task (traduzione, riassunto, classificazione) è formulato come un problema di testo-in-ingresso e testo-in-uscita.

## 6. Dal Calcolo al Testo: Strategie di Decoding

L'ultimo step è la trasformazione delle probabilità in parole. Esistono diverse strategie:
- **Greedy Decoding**: Sceglie sempre il token più probabile. È veloce ma spesso ripetitivo e suboptimal.
- **Beam Search**: Esplora più percorsi paralleli (beam width), mantenendo le sequenze con la probabilità globale più alta.
- **Stochastic Sampling**: Introduce varietà tramite il campionamento.
    - **Top-k**: Considera solo i $k$ token più probabili.
    - **Top-p (Nucleus)**: Considera l'insieme minimo di token che coprono una massa di probabilità $p$.
    - **Temperature**: Modifica la "piattezza" della distribuzione. Una temperatura bassa rende il modello deterministico, una alta lo rende più creativo e diversificato.
