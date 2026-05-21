# IR Evaluation Measures

Information Retrieval (IR) evaluation relies on various measures to quantify the effectiveness of a system. These measures differ in their mathematical properties and the measurement scales they belong to.

## Set-Based Measures
These measures focus on the set of retrieved documents regardless of their exact rank (though some incorporate rank).

- **Precision (P):** The proportion of retrieved documents that are relevant.
  $$\text{Precision} = \frac{|\text{Retrieved} \cap \text{Relevant}|}{|\text{Retrieved}|}$$
- **Recall (R):** The proportion of all relevant documents that were retrieved.
  $$\text{Recall} = \frac{|\text{Retrieved} \cap \text{Relevant}|}{|\text{Relevant}|}$$
- **F-measure (F):** The harmonic mean of Precision and Recall, providing a single score that balances both.

## Rank-Based Measures
These measures account for the position of relevant documents in the result list.

- **Average Precision (AP):** The arithmetic mean of precision values calculated at the rank of each relevant document.
- **Reciprocal Rank (RR):** The reciprocal of the rank of the first relevant document found ($1/rank_1$).
- **Discounted Cumulative Gain (DCG):** Sums the relevance of documents, discounted by the logarithm of their rank.
- **Rank-Biased Precision (RBP):** Models user persistence with a parameter $p$, calculating the probability that a user will find a relevant document given their patience.

## Scale Properties Summary

| Measure | Scale Type | Note |
|---|---|---|
| Precision | Interval | Transformation of SBTO |
| Recall | Interval | Transformation of SBTO |
| F-measure | Interval | Transformation of SBTO |
| RBP ($p=0.5$) | Interval | Transformation of RBTO |
| RBP ($p<0.5$) | Ordinal | |
| RR | Ordinal | Departs from intervalness as run length increases |
| AP | Ordinal/Other | Not ordinal wrt strong top-heaviness |
| DCG | Near-Interval | High correlation with interval scales |

## Choosing the Right Statistical Test
The scale type determines the appropriate test:
- **Ordinal Scale $\to$** Sign Test, Wilcoxon Rank Sum Test, Friedman Test.
- **Interval Scale $\to$** Student's t-Test, ANOVA, Wilcoxon Signed Rank Test.
