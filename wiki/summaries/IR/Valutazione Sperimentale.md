# IR - Valutazione Sperimentale

> "If you cannot measure it, you cannot improve it."

La valutazione in IR non riguarda l'efficienza algoritmica (tempo/spazio), ma l'**effettività**: la capacità del sistema di restituire documenti rilevanti.

## 1. Il [[Cranfield-Paradigm]]
Sviluppato negli anni '60, è lo standard per testare algoritmi in modo oggettivo e ripetibile. Si basa su una **collezione sperimentale** composta da una triade:
1. **Document Corpus**: Un set statico di documenti.
2. **Topics**: Rappresentazioni standardizzate dei bisogni informativi (Titolo, Descrizione, Narrativa).
3. **Relevance Judgments (qrels/Ground Truth)**: Valutazioni umane che indicano quali documenti sono rilevanti per quali topic.
    - **qrels**: Rappresentati come triple $\langle \text{query\_id}, \text{document\_id}, \text{relevance\_level} \rangle$. Il livello può essere binario (0/1) o graduale (es. 0-3).
    - **Ground Truth**: In IR, non è una verità assoluta ma una "verità percepita" basata su giudizi umani, poiché la pertinenza è una relazione soggetiva tra utente, query e documento.

**Vantaggio**: Permette il confronto diretto tra diversi sistemi (benchmark) in un ambiente controllato.

### Il Ruolo di [[TREC]] (Text REtrieval Conference)
Se Cranfield è la base teorica, **TREC** è l'implementazione pratica e standardizzata a livello mondiale. Organizzata dalla NIST, TREC definisce i formati standard per i file di output (`run`) e i giudizi (`qrels`), permettendo a ricercatori di tutto il mondo di competere e confrontare i propri algoritmi su corpora massivi e topic complessi.

---

## 2. Processo di Valutazione e Pooling
Poiché è impossibile per un umano valutare milioni di documenti, si utilizza il **Top-K Pooling**.

### Il Processo di Pooling
1. **Run Submission**: Diversi sistemi eseguono la ricerca e inviano i loro top-K risultati (RUN file).
2. **Creazione del Pool**: Si uniscono tutti i top-K di tutti i sistemi.
3. **Assessment**: Gli esperti valutano *solo* i documenti presenti nel pool. 
    - **Assunzione Fondamentale**: Tutti i documenti non presenti nel pool (e quindi non giudicati) sono assunti come **non rilevanti**.

### Qualità del Pool e Rischi
Un pool è valido se è **Rappresentativo** e **Stabile**.
- **Leave-one-out test**: Si rimuove il contributo di un sistema dal pool e si ricalcola il ranking. Se il ranking dei restanti sistemi non cambia significativamente (misurato tramite [[Tau di Kendall]]), il pool è stabile.

**Rischi legati a un pool di scarsa qualità**:
- **Bias di Selezione**: Se tutti i sistemi usati per il pooling mancano la stessa categoria di documenti rilevanti, questi non entreranno mai nel pool, portando a una Recall artificialmente alta.
- **Sottostima della Recall**: Un pool troppo piccolo rischia di non includere documenti rilevanti "difficili", rendendo la valutazione incompleta.
- **Overfitting**: I sistemi che hanno contribuito alla creazione del pool tendono a sembrare migliori di sistemi testati a posteriori.

---
 
## 3. Approcci alla Valutazione: System-Centric vs User-Centric
Esistono due filosofie principali per misurare l'efficacia di un sistema di IR:

1. **Valutazione System-Centric (Offline)**:
    - **Focus**: Accuratezza del ranking rispetto a un dataset statico.
    - **Metodo**: Utilizza corpora, topic e qrels (Paradigma di Cranfield).
    - **Vantaggi**: Rapida, ripetibile, costi contenuti, ideale per il tuning algoritmico.
    - **Limite**: Non tiene conto dell'interazione reale e della psicologia dell'utente.

2. **Valutazione User-Centric (Online)**:
    - **Focus**: Soddisfazione dell'utente e utilità reale.
    - **Metodo**: Analisi di log di ricerca, A/B testing, Click-Through Rate (CTR), tempo di permanenza, interviste.
    - **Vantaggi**: Misura l'impatto reale dell'interfaccia e l'efficacia del recupero nel mondo reale.
    - **Limite**: Costosa, lenta, difficile da replicare e soggetta a rumore (es. click accidentali).

---

 
## 4. Metriche di Valutazione

### A. Metriche Set-Based (Unordered Bucket)
Considerano i risultati come un insieme, ignorando l'ordine.
(B: tutti i documenti recuperati dal sistema)
(A: tutti i documenti rilevanti esistenti nel corpus della specifica query)
(A $\cap$ B: documenti sia rilevanti che recuperati)
- **[[Precision]]**: Proporzione di documenti recuperati che sono effettivamente rilevanti.
  $$P = \frac{|A \cap B|}{|B|}$$
- **[[Recall]]**: Proporzione di documenti rilevanti totali che sono stati recuperati.
  $$R = \frac{|A \cap B|}{|A|}$$
- **[[F-Measure]]**: Media armonica tra Precision e Recall (usata per avere un unico score).
   $$F = \frac{2 \cdot P \cdot R}{P + R} = \frac{2 \cdot |A \cap B|}{|A|+|B|}$$

#### Il Trade-off tra Precision e Recall
In quasi tutti i sistemi di IR, Precision e Recall sono in **conflitto**:
- **Aumentare la Recall** (recuperare più documenti rilevanti) solitamente comporta l'inserimento di più "rumore" (documenti non rilevanti), facendo **scendere la Precision**.
- **Aumentare la Precision** (essere molto selettivi) comporta l'esclusione di documenti potenzialmente rilevanti, facendo **scendere la Recall**.

**La Curva Precision-Recall (P-R Curve)**:
È un grafico che rappresenta la Precision in funzione della Recall al variare della soglia di recupero (o della profondità $K$). 
- Un sistema ideale ha una curva che rimane alta (vicino a 1) per tutta la durata della Recall.
- L'area sotto questa curva (**AUC-PR**) è una metrica globale per valutare la qualità del sistema indipendentemente da un singolo valore di $K$.

![Esempio Curva P-R|281](https://upload.wikimedia.org/wikipedia/commons/2/26/Precisionrecall.svg)
*(Immagine rappresentativa: la Precision tende a diminuire all'aumentare della Recall)*

#### Focus: La Recall Base (RB)
La **Recall Base** è il numero totale di documenti rilevanti esistenti per un determinato topic all'interno del corpus (estratto dal Ground Truth/qrels). È il "soffitto" teorico del sistema.

**Esempio Pratico**:
Se per il Topic "Quokka" esistono solo 2 documenti rilevanti in tutto il corpus $\rightarrow \text{RB} = 2$.
- Se il sistema restituisce 10 documenti ($\text{P@10}$), anche se i primi 2 sono perfetti, la precisione sarà $2/10 = 20\%$.
- In questo caso, il 20% è un risultato perfetto perché limitato dalla $\text{RB}$.

---

### B. Metriche Rank-Based (Ordered List)
Considerano la posizione del documento nel ranking.


#### [[P@K]]
Precision calcolata solo sui primi $K$ documenti.
- **Limite**: È fortemente vincolata dalla **Recall Base (RB)**. Se $\text{RB}=8$, $\text{P@10}$ non potrà mai superare l'80%, anche con un sistema perfetto.

#### [[R-Precision]] ($\text{R-prec}$)
Precision calcolata esattamente al rango pari alla Recall Base ($\text{P@RB}$). È l'unico punto teorico dove Precision e Recall possono essere simultaneamente al 100%.
- avendo ora una $K$ dinamica pari alla $RB$, il confronto tra query diverse è più equo.
#### [[Average Precision]] ($\text{AP}$) e [[MAP]]
L'$\text{AP}$ calcola la precisione solo nei punti in cui viene trovato un documento rilevante:
$$\text{AP} = \frac{1}{\text{RB}} \sum_{k \in \text{Rel}} P(k)$$
La **Mean Average Precision ($\text{MAP}$)** è la media delle $\text{AP}$ su tutti i topic del corpus. È il gold standard per riassumere l'efficacia globale.

#### [[MRR]] ($\text{MRR@K}$)
Misura la posizione del **primo** documento rilevante. È ideale per sistemi di *Known-Item Search* o *Question Answering*.
- **Reciprocal Rank (RR)**: $\text{RR} = \frac{1}{\text{rank del primo doc rilevante}}$. Se non ci sono rilevanti entro $K$, $\text{RR} = 0$.
- **MRR**: Media dei RR su tutte le query.
$$\text{MRR} = \frac{1}{|Q|} \sum_{i=1}^{|Q|} \frac{1}{\text{rank}_i}$$

> [!IMPORTANT] **Differenza con MAP**
    > Mentre la MAP considera tutti i documenti rilevanti, l'MRR si cura solo di quanto velocemente l'utente trova la prima risposta corretta.


#### [[DCG]]
Utilizzata per rilevanze multi-graduate (es. "molto rilevante", "poco rilevante").
($i$: posizione nel ranking)
($r_i$: rilevanza del doc. alla pos. $i$, ad esempio da 0 a 3; prima era 0/1)
$$\text{DCG}(K) = \sum_{i=1}^K \frac{r_i}{\log_2(i+1)}$$
Per confrontare sistemi diversi, si usa la **[[nDCG]] (normalized DCG)**, dividendo il $\text{DCG}$ ottenuto per il $\text{DCG}$ di un ranking ideale ($\text{iDCG}$).


#### [[RBP]]
Modella il comportamento dell'utente come un automa che decide se continuare a scorrere i risultati con probabilità $p$ (persistenza).
$$\text{RBP} = (1-p) \sum_{m=1}^N p^{m-1} r_m$$
- $p$ alto $\rightarrow$ utente paziente.
- $p$ basso $\rightarrow$ utente impaziente.

---

## 5. Strumenti di Valutazione
- **`trec_eval`**: Tool standard in C per calcolare metriche partendo da file `qrels` (ground truth) e `run.txt` (output sistema).
- **`ir_measures`**: Libreria Python alternativa a `trec_eval`.
- **`ir_datasets`**: Hub per scaricare e gestire corpora sperimentali.

---
Tabella Riassuntiva per l'esame
![![wiki/summaries/IR/#*Table]]