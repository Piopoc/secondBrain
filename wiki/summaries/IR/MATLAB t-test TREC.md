---
date: 2026-05-08
source: [[raw/10/image6.png]]
tags: [matlab, ir-evaluation, implementation]
---

# Implementazione t-test in MATLAB (TREC)

Questa guida descrive il workflow per l'implementazione pratica di un [[concepts/t-test di Student Paired|t-test]] per confrontare sistemi di Information Retrieval utilizzando dati [[entities/TREC|TREC]].

## Workflow di Analisi

### 1. Setup del Dataset
Il punto di partenza è l'importazione delle score di **Average Precision (AP)**, organizzate in una matrice `[topics x runs]`.
```matlab
load('../../data/T08/ap.mat')
measure = ap;
```

### 2. Calcolo e Ordinamento Performance
Per ogni run viene calcolata la **MAP (Mean Average Precision)**, che rappresenta la media delle AP sui topic. I run vengono poi ordinati in modo decrescente per facilitare l'analisi.
```matlab
m = mean(measure); % Calcola MAP per ogni run
[~, idx] = sort(m, 'descend'); % Ordina indici decrescenti
measure = measure(:, idx); % Riordina matrice score
runs = runs(idx); % Riordina nomi run
```

### 3. Visualizzazione con Box Plot
L'uso di `boxchart` permette di visualizzare la distribuzione delle AP di ogni run. L'ordinamento per MAP decrescente permette di identificare rapidamente la tendenza centrale, la dispersione e la sovrapposizione tra i sistemi. Vedi [[concepts/Box Plot]].

### 4. Esecuzione del t-test
Esistono due modi per eseguire il test in MATLAB:

**A. Metodo Rapido (Funzione integrata):**
```matlab
[~, p] = ttest(measure(:, r1), measure(:, r2))
fprintf("Run %s vs %s: p-value %f", runs(r1), runs(r2), p)
```

**B. Metodo Passo-Passo (Logica manuale):**
Per ogni coppia di sistemi (X, Y):
1. Calcolo differenze: `D = X - Y`
2. Media differenze: `mu_D = mean(D)`
3. Varianza differenze: `var_D = var(D)`
4. Test Statistic: `t_stat = mu_D / sqrt(var_D / n)`. Vedi [[concepts/Test Statistic]].
5. p-value: `p = 2 * (1 - tcdf(abs(t_stat), df))` dove $df = n-1$. Vedi [[concepts/p-value]].

## Interpretazione dei Risultati (Simulazione)

L'analisi di tre sistemi (X, Y, Z) con diverse distribuzioni mostra i possibili esiti del test:

| Confronto | Realtà | Risultato Test | Conclusione |
| :--- | :--- | :--- | :--- |
| **X vs Y** | Stessa dist. | $p > \alpha$ | ✅ **Corretta** (Vero Negativo) |
| **X vs Z** | Dist. diverse | $p < \alpha$ | ✅ **Corretta** (Vero Positivo) |
| **Y vs Z** | Dist. diverse | $p > \alpha$ | ❌ **Errore Tipo II** (Falso Negativo) |

L'ultimo caso (Y vs Z) evidenzia come, nonostante i sistemi siano diversi, il test possa non rilevare la differenza a causa di una [[concepts/Potenza Statistica|potenza statistica insufficiente]] (campione troppo piccolo o varianza troppo alta). Vedi [[concepts/Errori Statistici]].

Vedi anche: [[concepts/t-test di Student Paired]], [[concepts/Box Plot]], [[concepts/Errori Statistici]], [[summaries/IR/IR - Statistical Testing|IR - Statistical Testing]]
