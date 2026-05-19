# 📝 Esercizi: Statistical Testing & MATLAB (IR)

Questo documento contiene una serie di esercizi progettati per consolidare le nozioni di testing statistico applicato all'Information Retrieval, con particolare focus sull'implementazione in MATLAB e l'analisi di dati TREC.

---

## 📊 Categoria 1: Statistica Descrittiva e Box Plot

### Esercizio 1.2: Calcolo della MAP (Mean Average Precision)
**Problema**: Hai 3 topic e 2 sistemi (S1, S2). Le Average Precision (AP) sono:
- **S1**: $[0.8, 0.4, 0.6]$
- **S2**: $[0.5, 0.7, 0.5]$

Calcola la MAP per entrambi i sistemi e determina quale sia il migliore in termini di media.

**Soluzione Passo-Passo**:
1. **MAP S1**: $\frac{0.8 + 0.4 + 0.6}{3} = \frac{1.8}{3} = 0.60$
2. **MAP S2**: $\frac{0.5 + 0.7 + 0.5}{3} = \frac{1.7}{3} \approx 0.566$
3. **Conclusione**: S1 ha una MAP superiore a S2. Tuttavia, per sapere se questa differenza è significativa, è necessario procedere con un t-test.


---

## 🧪 Categoria 2: Test di Ipotesi e p-value

### Esercizio 2.1: La Decisione Statistica
**Problema**: Vuoi confrontare due sistemi di ranking. Imposti un livello di significatività $\alpha = 0.05$. Dopo aver eseguito un [[concepts/t-test di Student Paired]], ottieni un $p\text{-value} = 0.032$.
1. Qual è l'ipotesi nulla $H_0$ in questo contesto?
2. Qual è la decisione finale?
3. C'è il rischio di commettere un errore? Se sì, di che tipo?

**Soluzione Passo-Passo**:
1. **Definizione $H_0$**: L'ipotesi nulla assume che non vi sia alcuna differenza reale tra le performance medie dei due sistemi ($\mu_{S1} = \mu_{S2}$). Qualsiasi differenza osservata è dovuta al caso.
2. **Regola di Decisione**: Poiché $p\text{-value} (0.032) < \alpha (0.05)$, l'evidenza è sufficiente per **rigettare $H_0$**.
3. **Conclusione**: La differenza tra i due sistemi è **statisticamente significativa**.
4. **Analisi dell'Errore**: Poiché abbiamo rigettato $H_0$, esiste la possibilità di aver commesso un **[[concepts/Errori Statistici|Errore di Tipo I]] (Falso Positivo)**: abbiamo dichiarato che i sistemi sono diversi quando in realtà non lo erano. La probabilità di questo errore è esattamente $\alpha$.

---

## 💻 Categoria 3: Implementazione MATLAB e t-test

### Esercizio 3.1: Calcolo Manuale del t-test (Senza Computer)
**Problema**: Considera i seguenti dati di AP per due sistemi su 4 topic:
- **S1**: $[0.8, 0.6, 0.7, 0.9]$
- **S2**: $[0.7, 0.5, 0.6, 0.8]$

Calcola manualmente la [[concepts/Test Statistic]] ($t_{stat}$).

**Soluzione Passo-Passo**:
1. **Calcolo differenze ($D = S1 - S2$)**:
   $D = [0.1, 0.1, 0.1, 0.1]$
   *(Nota: In un esame i numeri potrebbero variare, es. $D = [0.1, 0.2, 0.0, 0.1]$)*.
2. **Media differenze ($\mu_D$)**:
   $\mu_D = \frac{0.1 + 0.1 + 0.1 + 0.1}{4} = 0.1$
3. **Varianza differenze ($\text{var}_D$)**:
   $\text{var}_D = \frac{\sum (D_i - \mu_D)^2}{n-1} = \frac{0+0+0+0}{3} = 0$
   *(Se $D$ fosse stato $[0.1, 0.2, 0.0, 0.1]$, avresti $\mu_D=0.1$ e $\text{var}_D = \frac{0^2 + 0.1^2 + (-0.1)^2 + 0^2}{3} = \frac{0.02}{3} \approx 0.0066$)*.
4. **Calcolo $t_{stat}$**:
   $t_{stat} = \frac{\mu_D}{\sqrt{\text{var}_D / n}} = \frac{0.1}{\sqrt{0/4}} \rightarrow \infty$
   *(Con i dati d'esempio $\text{var}_D=0.0066$: $t_{stat} = \frac{0.1}{\sqrt{0.0066/4}} = \frac{0.1}{0.0406} \approx 2.46$)*.

### Esercizio 3.2: Decisione tramite Tabella t di Student
**Problema**: Hai calcolato un $t_{stat} = 2.46$ con un campione di $n=4$ topic. Il livello di significatività è $\alpha = 0.05$ (test a due code).
Consultando la tabella t di Student, trovi che per $df = 3$ e $\alpha = 0.05$, il valore critico è $t_{crit} = 3.182$.
**Il risultato è statisticamente significativo?**

**Soluzione Passo-Passo**:
1. **Confronto**: $|t_{stat}| = 2.46$ vs $t_{crit} = 3.182$.
2. **Regola**: Se $|t_{stat}| > t_{crit} \rightarrow$ Rifiuto $H_0$.
3. **Risultato**: $2.46 < 3.182 \rightarrow$ **Non rifiuto $H_0$**.
4. **Conclusione**: Nonostante la media di S1 sia superiore, la differenza non è statisticamente significativa per questo campione.


---

## 🚀 Categoria 4: Caso Integrato (Scenario TREC)

### Esercizio 4.1: Workflow Completo di Valutazione
**Problema**: Sei un ricercatore che ha sviluppato un nuovo algoritmo di ranking. Hai i file `qrels` (ground truth) e i file `run` di tre sistemi: il tuo (**MySys**), un baseline (**Base**) e lo stato dell'arte (**SOTA**).
Descrivi l'intero workflow, dai dati grezzi alla conclusione statistica, citando i concetti e i tool utilizzati.

**Soluzione Passo-Passo**:
1. **Estrazione Metriche**: Utilizzo di `trec_eval` o `ir_measures` per calcolare l'**Average Precision (AP)** per ogni topic per i tre sistemi.
2. **Analisi Descrittiva**: Calcolo della **[[MAP]]** (Mean Average Precision) per ogni sistema e ordinamento decrescente.
3. **Analisi Visiva**: Creazione di un **[[concepts/Box Plot]]** per confrontare le distribuzioni di AP. Se i box di **MySys** e **SOTA** si sovrappongono molto, il t-test sarà cruciale.
4. **Testing Statistico**:
   - Esecuzione di un **[[concepts/t-test di Student Paired]]** tra **MySys** e **Base** per confermare il miglioramento.
   - Esecuzione del test tra **MySys** e **SOTA**.
5. **Gestione Comparazioni Multiple**: Poiché stiamo facendo più test (MySys vs Base, MySys vs SOTA, Base vs SOTA), applichiamo la **[[concepts/Correzione di Bonferroni]]** dividendo $\alpha$ per il numero di coppie (3), portando $\alpha_{adj} = 0.05 / 3 \approx 0.0167$.
6. **Conclusione**: Se $p < 0.0167$ nel confronto MySys vs SOTA, possiamo affermare con confidenza che il nuovo algoritmo è significativamente migliore dello stato dell'arte.

---

## 🧠 Domande di Riflessione (Quick Check)

1. **Perché usiamo il t-test "appaiato" (paired) e non quello indipendente in IR?**
   - *Risposta*: Perché valutiamo i sistemi sugli **stessi topic**. La variabilità tra i topic (alcuni sono più facili di altri) è enorme; l'appaiamento elimina questa varianza, focalizzandosi solo sulla differenza di performance tra i sistemi.
2. **Cosa succede se aumento drasticamente il numero di topic ($n$) nel mio dataset TREC?**
   - *Risposta*: Aumenta la **[[concepts/Potenza Statistica]]**. Sarò in grado di rilevare differenze più piccole (anche se forse irrilevanti a livello pratico) come statisticamente significative.
3. **Se il p-value è 0.06 e $\alpha=0.05$, posso dire che i sistemi sono uguali?**
   - *Risposta*: No. Posso solo dire che **non ho prove sufficienti per rigettare $H_0$**. Non "accetto" mai l'ipotesi nulla.
