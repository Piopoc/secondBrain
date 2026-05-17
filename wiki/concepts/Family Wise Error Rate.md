---
date: 2026-05-08
source: [[raw/10/image4.png]]
tags: [statistics, multiple-comparisons]
---

# Family-Wise Error Rate (FWER)

Il **Family-Wise Error Rate** (FWER) è la probabilità di commettere **almeno un** Errore di Tipo I quando si effettuano più confronti statistici contemporaneamente (comparazioni multiple).

## Il Problema delle Comparazioni Multiple
Se confrontiamo $c$ sistemi, avremo $m = \binom{c}{2}$ coppie possibili. Se ogni test ha un livello di significatività $\alpha$, la probabilità di non sbagliare in un singolo test è $(1-\alpha)$. 
Se i test sono indipendenti, la probabilità di non commettere alcun errore in $m$ test è:
$$P(\text{Nessun Errore Tipo I}) = (1-\alpha)^m$$

## Formula del FWER
Il FWER è il complemento della probabilità di non commettere errori:
$$\text{FWER} = 1 - (1-\alpha)^m$$

## Esempio Numerico ($\alpha = 0.05$)
| Numero di comparazioni ($m$) | FWER |
| :--- | :--- |
| 1 | 5% |
| 5 | 23% |
| 10 | 40% |

L'aumento esponenziale del FWER rende necessario l'uso di correzioni (come la correzione di Bonferroni) per mantenere il tasso di errore globale sotto controllo.

Vedi anche: [[Errori_Statistici]], [[Livello_di_Significativita]], [[Lezione_24_Statistical_Testing_Knowledge_Graphs]]
