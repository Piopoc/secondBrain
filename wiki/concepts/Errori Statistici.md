---
date: 2026-05-08
source: [[raw/10/image3.png]]
tags: [statistics, error-analysis]
---

# Errori Statistici e Power

Nel testing statistico, le conclusioni tratte dai dati possono non coincidere con la realtà. Si definiscono quindi due tipi di errore e il concetto di potenza.

## Matrice degli Errori

| Realtà $\downarrow$ | Non rifiuto $H_0$ (non signif.) | Rifiuto $H_0$ (signif.) |
| :--- | :--- | :--- |
| **$H_0$ vera** (Sistemi equivalenti) | ✅ Conclusione corretta (prob. $1-\alpha$) | ❌ **Errore Tipo I** (Falso Positivo, prob. $\alpha$) |
| **$H_0$ falsa** (Sistemi diversi) | ❌ **Errore Tipo II** (Falso Negativo, prob. $\beta$) | ✅ **Power** (Conclusione corretta, prob. $1-\beta$) |

## Dettagli

### 1. Errore di Tipo I (Falso Positivo)
Si verifica quando si afferma che i sistemi sono diversi mentre in realtà sono equivalenti. 
- **Probabilità**: $\alpha$ (livello di significatività).
- **Gravità**: È considerato l'errore più grave poiché porta a decisioni sbagliate con conseguenze concrete (es. lanciare un prodotto inefficace).

### 2. Errore di Tipo II (Falso Negativo)
Si verifica quando non si riesce a rilevare una differenza che in realtà esiste (si dice che i sistemi sono equivalenti quando sono diversi).
- **Probabilità**: $\beta$ (tipicamente $\beta = 0.20$).
- **Gravità**: È visto come un'occasione persa, generalmente meno grave del Falso Positivo. Analogo medico: scartare un farmaco efficace.

**Esempio Pratico (Simulazione MATLAB)**:
In un confronto tra due sistemi Y e Z con distribuzioni diverse, se il p-value risultante è $0.18$ (con $\alpha=0.05$), il test conclude che non c'è differenza significativa. Poiché in realtà i sistemi sono diversi, si è commesso un **Errore di Tipo II**. Questo accade tipicamente quando il test non ha abbastanza **Power** (potenza statistica).

### 3. Power (Potenza Statistica)
È la probabilità di rigettare correttamente $H_0$ quando l'ipotesi è effettivamente falsa.
- **Probabilità**: $1 - \beta$.
- **Target**: Tipicamente $\text{Power} \ge 0.80$.

Vedi anche: [[Potenza_Statistica]], [[Livello_di_Significativita]], [[Test_di_Ipotesi]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
