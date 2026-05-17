# IR - Privacy e Obfuscation

L'obiettivo della **Query Obfuscation** è permettere a un utente di ==ottenere risultati rilevanti da un sistema di ricerca== (IRS) ==senza rivelare l'esatta natura della propria query==, proteggendo la privacy.

## 1. Fondamenti di Privacy
La privacy è analizzata da due prospettive:
- **Etica/Legale**: Riferimento al **GDPR** e al diritto di controllare i propri dati.
- **Tecnica**:
	- **Security**: Chi può accedere ai dati.
	- **Privacy**: Cosa può essere dedotto dai dati.

### Il Flusso di Obfuscation
In un sistema standard, l'utente invia la query $\rightarrow$ l'IRS restituisce i documenti. In un sistema con obfuscation:
`Utente (SAFE)` $\rightarrow$ `Meccanismo di Obfuscation` $\rightarrow$ `Query Offuscata` $\rightarrow$ `IRS (UNSAFE)` $\rightarrow$ `Documenti Ranked` $\rightarrow$ `Post-filtering (SAFE)` $\rightarrow$ `Utente`.

---

## 2. Meccanismi di Obfuscation

### Pipeline di Obfuscation (3 Fasi)
1. **Preprocessing**: Preparazione del testo della query.
2. **Distortion**: Scelta dei termini da offuscare.
3. **Selection**: Selezione dei termini sostitutivi.

### Approcci Euristici
Utilizzo di risorse come **WordNet** per sostituire termini con sinonimi o iperonimi.
- **Trade-off**: 
	- $\text{Alta Privacy} \rightarrow \text{Bassa Utility}$ (la query diventa troppo vaga).
	- $\text{Bassa Privacy} \rightarrow \text{Alta Utility}$ (i risultati sono precisi ma la query è quasi trasparente).

---

## 3. Modelli Matematici di Privacy

### K-Anonymity
Utilizzata principalmente per dati tabulari. Un dataset soddisfa la [[K-Anonymity]] se ogni individuo non è distinguibile da almeno $K-1$ altri individui rispetto a un set di **quasi-identificatori**.

### [[Differential Privacy]] (DP)
Un'operazione è $\epsilon$-differenzialmente privata se l'aggiunta o la rimozione di un singolo elemento dal dataset non altera significativamente la distribuzione dell'output.
- **Meccanismo**: Aggiunta di rumore statistico, tipicamente rumore Gaussiano $N(0, \sigma)$.
- **Budget di Privacy ($\epsilon$)**:
	- $\epsilon$ piccolo $\rightarrow$ Alta privacy (più rumore).
	- $\epsilon$ grande $\rightarrow$ Bassa privacy (meno rumore).

### Metric-DP e Embedding
Poiché le query di testo sono spesso convertite in **[[Word-Embedding]]** (vettori densi), la DP tradizionale non è sufficiente. Si usa la **[[Metric-DP]]**, che aggiunge rumore direttamente nello spazio vettoriale degli embedding per proteggere la "sfumatura di significato" del testo.

---

## 4. [[KCMP]] (Calibrated Multivariate Perturbations)
Il metodo KCMP implementa l'offuscation in tre step:
1. **Preprocessing**: [[Tokenization]] della query e calcolo degli embedding.
2. **Perturbazione**: Calcolo di un vettore di rumore basato su una densità di probabilità per ogni parola.
3. **Selezione**: Scelta della parola offuscata che meglio approssima il vettore perturbato.

**Limitazioni di KCMP**:
- Non considera la distribuzione globale degli embedding (risolvibile con norme di Mahalanobis).
- Rischio che una parola venga offuscata con se stessa.
- Campionamento indipendente delle parole (ignora il contesto).

---

## 5. Valutazione dell'Obfuscation
Per misurare l'efficacia di un sistema di offuscamento si utilizzano:
- **[[Cosine-Similarity]]**: Misura quanto il vettore della query offuscata sia vicino a quello originale.
- **[[Jaccard Similarity]]**: Proporzione di parole comuni tra il testo originale e quello offuscato.
- **Metriche di Machine Translation**: Utilizzo del testo originale come riferimento per valutare la perdita di significato.
