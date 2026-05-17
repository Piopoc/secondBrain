---
date: 2026-05-08
source:
  - - raw/10/image0.png
tags:
  - statistical-testing
  - search-engines
  - box-plot
---

# Sintesi: Statistical Testing & Knowledge Graphs (Lezione 24)

Questa lezione, tenuta da Stefano Marchesin per il corso di Search Engines (Prof. Ferro) presso l'Università di Padova, introduce gli strumenti di testing statistico per la valutazione delle performance dei sistemi di ricerca.

---
## Fondamenti Statistici (Note Manuali)
La lezione richiama concetti di statistica descrittiva e inferenziale:
- **Media Campionaria ($\hat{\mu}_x$)**: $\frac{1}{m} \sum_{i=1}^m x_i$
- **Varianza Campionaria ($\hat{\sigma}_x^2$)**: $\frac{1}{m-1} \sum_{i=1}^m (x_i - \hat{\mu}_x)^2$ (con m-1 gradi di libertà).
- **Teorema del Limite Centrale (CLT)**: Stabilisce che la media campionaria segue una distribuzione normale:
    - $\hat{\mu}_x \sim \mathcal{N}(\mu_x, \frac{\hat{\sigma}_x^2}{m})$
    - La variabile standardizzata $\frac{\hat{\mu}_x - \mu_x}{\hat{\sigma}_x / \sqrt{m}}$ segue una distribuzione $\mathcal{N}(0, 1)$.
---

## Punti Chiave

### 1. Box Plot
Il [[concepts/Box Plot|Box Plot]] è uno strumento grafico fondamentale per riassumere la distribuzione di un insieme di dati e confrontare le performance di più sistemi su collezioni di query/topic.

**Perché usarlo in IR?**
Permette di andare oltre la semplice media, osservando:
- La forma della distribuzione delle performance (es. AP, nDCG) su diversi topic.
- Il grado di sovrapposizione tra due sistemi (per capire se sono distinguibili).
- La presenza di topic "difficili" (outlier negativi) o "facili" (outlier positivi).

**Relazione con la Distribuzione Normale:**
In una distribuzione normale perfetta:
- $Q1 \approx \mu - 0.6745\sigma$
- $Q3 \approx \mu + 0.6745\sigma$
- I baffi coprono circa il 99% dei dati ($\approx \pm 2.698\sigma$).

**Struttura e Componenti:**
- **Box**: Rappresenta l'intervallo tra il primo quartile (Q1, 25°) e il terzo quartile (Q3, 75°). Contiene il 50% centrale dei dati.
- **Mediana (Q2)**: Il 50° percentile, indica il valore centrale della distribuzione.
- **IQR (Inter-Quartile Range)**: Calcolato come $Q3 - Q1$. È una misura di dispersione robusta. Vedi [[concepts/IQR]].
- **Whiskers (Baffi)**:
    - Superiore: $Q3 + 1.5 \cdot IQR$
    - Inferiore: $Q1 - 1.5 \cdot IQR$
- **Outliers**: Dati che cadono al di fuori dei baffi.

### 2. Significatività Statistica e Test di Ipotesi
Il problema centrale è determinare se la differenza di performance tra due sistemi (es. Sistema A con MAP=0.42 vs Sistema B con MAP=0.39) sia **strutturale** (reale) o **accidentale** (dovuta al rumore del campionamento casuale dei topic, es. collezioni [[entities/TREC|TREC]]). Vedi [[concepts/Significativita Statistica]].

**Il Framework del Test di Ipotesi (Statistical Hypothesis Testing):**
È il metodo formale per condurre l'inferenza statistica dai dati, confrontando due ipotesi. Vedi [[concepts/Test di Ipotesi]].
- **Ipotesi Nulla ($H_0$)**: L'ipotesi "conservativa". Assume che non vi sia differenza reale tra i sistemi ($\mu_A = \mu_B$). L'obiettivo del test è solitamente quello di **rigettare** $H_0$. **Nota fondamentale**: In statistica $H_0$ non si "accetta" mai, si può solo rigettare o non rigettare. Vedi [[concepts/Ipotesi Nulla e Alternativa]].
- **Ipotesi Alternativa ($H_1$)**: L'ipotesi che vogliamo dimostrare. Assume che esista una differenza reale tra le performance medie ($\mu_A \neq \mu_B$). Vedi [[concepts/Ipotesi Nulla e Alternativa]].

**Meccanica del Test:**
1. **Livello di Significatività ($\alpha$)**: È la probabilità di errore che siamo disposti ad accettare. Vedi [[concepts/Livello di Significativita]].
2. **Test Statistic ($T_{stat}$)**: Un numero calcolato dai dati che riassume quanto è "grande" la differenza osservata. Vedi [[concepts/Test Statistic]].
3. **Valore Critico ($t_{crit}$)**: Il valore della distribuzione che definisce la soglia di rigetto. Vedi [[concepts/Valore Critico]].

**Regola di Decisione:**
- Se $|T_{osservato}| > t_{crit} \rightarrow$ **Rifiuto $H_0$** (la differenza è statisticamente significativa).
- Se $|T_{osservato}| \le t_{crit} \rightarrow$ **Non rifiuto $H_0$** (non c'è evidenza sufficiente per dire che i sistemi siano diversi).

**Il p-value:**
È la probabilità di osservare una test statistic almeno altrettanto estrema di quella ottenuta, assumendo che $H_0$ sia vera. Vedi [[concepts/p-value]].
- **Interpretazione**: Se $p\text{-value} < \alpha \rightarrow$ Rifiuto $H_0$.
- **Vantaggi rispetto al Valore Critico**: È auto-contenuto, portabile e più informativo.

**Tipi di Errore e Power:**
La conclusione del test può divergere dalla realtà. Vedi [[concepts/Errori Statistici]].
- **Errore di Tipo I (Falso Positivo)**: Rifiutare $H_0$ quando è vera.
- **Errore di Tipo II (Falso Negativo)**: Non rigettare $H_0$ quando è falsa.
- **Power (Potenza Statistica)**: Probabilità di rigettare correttamente $H_0$ quando è falsa. Vedi [[concepts/Potenza Statistica]].
    - **Come aumentare il Power?** Aumentando il numero di campioni $n$.
    - **Attenzione**: Con $N$ enormi, si possono rilevare differenze statisticamente significative ma **praticamente irrilevanti** (p-hacking).

**Comparazioni Multiple e Family-Wise Error Rate (FWER):**
Quando si confrontano più di due sistemi, il numero di coppie possibili cresce rapidamente. Vedi [[concepts/Family Wise Error Rate]].
- **Il problema**: L'accumulo di probabilità di errore di Tipo I.
- **FWER**: La probabilità di commettere **almeno un** Errore di Tipo I tra tutte le comparazioni.

**Soluzioni per le Comparazioni Multiple:**
1. **Correzione di Bonferroni**: Metodo semplice ma conservativo. Vedi [[concepts/Correzione di Bonferroni]].
2. **ANOVA (Analysis of Variance)**: Test globale per verificare se almeno una delle medie è diversa. Vedi [[concepts/ANOVA]].
3. **Tukey HSD (Honestly Significant Difference)**: Test post-hoc per identificare quali coppie differiscono. Vedi [[concepts/Tukey HSD Test]].

**Analisi della Varianza (ANOVA):**
L'ANOVA scompone la varianza totale in Effetto Sistema ed Effetto Errore.
- **F-test**: La statistica $F_{stat}$ segue una distribuzione F. Vedi [[concepts/F-test]].
- **Assunzioni**: Indipendenza, Normalità e [[concepts/Omoschedasticita|Omoschedasticità]].

**Il t-test di Student Appaiato (Paired t-test):**
Utilizzato per confrontare due sistemi sulle stesse query/topic. Vedi [[concepts/t-test di Student Paired]].
1. **Assunzioni**: Indipendenza, Normalità e Omoschedasticità.
2. **Procedura**: Calcolo differenze $\rightarrow$ Media e Varianza delle differenze $\rightarrow$ Test Statistic.
3. **Distribuzione e Decisione**: Segue una distribuzione t di Student con $n-1$ [[concepts/Gradi_di_Liberta|gradi di libertà]].

**Confronto CLT vs t-test:**
- **CLT**: Varianza della **popolazione** $\rightarrow$ Distribuzione **Normale**. Vedi [[concepts/Teorema del Limite Centrale]].
- **t-test**: Varianza **campionaria** $\rightarrow$ Distribuzione **t di Student**.

**Implementazione Pratica (MATLAB su TREC):**
Workflow: Caricamento dati $\rightarrow$ Analisi Descrittiva (MAP) $\rightarrow$ Visualizzazione (Box Plot) $\rightarrow$ Testing (t-test). Vedi [[summaries/IR/IR - MATLAB t-test TREC|IR - MATLAB t-test TREC]].

**Test a due code (Two-tailed)**: Si usa quando non si assume a priori quale sistema sia migliore.
