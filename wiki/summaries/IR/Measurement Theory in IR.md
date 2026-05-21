# Measurement Theory in Information Retrieval

## Overview
[[Measurement Theory in IR]] addresses the fundamental question: **What kind of measurement scales do IR evaluation measures actually constitute?** This is critical because the scale type determines which mathematical and statistical operations (like computing a mean) are empirically meaningful.

## Key Theoretical Framework
The field relies on the [[Representational Measurement Theory]], which maps empirical relations (like "Run A is better than Run B") to numerical values. A central challenge in IR is the lack of a natural empirical ordering, as noted by [[C. J. van Rijsbergen]], making IR measures "artificial" by nature.

## Measurement Scales in IR
Based on [[S. S. Stevens]]' classification, IR measures are analyzed as:
- **Nominal:** Labels/Types.
- **Ordinal:** Relative order (e.g., Rank).
- **Interval:** Equal differences (e.g., Temperature, and some IR measures).
- **Ratio:** Absolute zero (e.g., Duration).

### Interval Scale Measures
The theory identifies two primary interval scale constructions:
1. **[[Set-Based Total Order (SBTO)]]:** Based on total relevance mass. [[IR Evaluation Measures|Precision]], [[IR Evaluation Measures|Recall]], and [[IR Evaluation Measures|F-measure]] are affine transformations of SBTO and thus are interval scales.
2. **[[Rank-Based Total Order (RBTO)]]:** Based on strong top-heaviness. [[IR Evaluation Measures|RBP]] with $p=0.5$ is an interval scale.

### Ordinal Scale Measures
Many common measures, such as [[IR Evaluation Measures|Reciprocal Rank (RR)]] and [[IR Evaluation Measures|Average Precision (AP)]], are primarily ordinal. Applying interval-scale statistics (like the t-test) to these measures can produce results that are not invariant under permissible transformations, rendering them [[Meaningfulness|meaningless]].

## The Multi-Graded Challenge
When moving from binary to **multi-graded relevance**, the analysis becomes more complex. Many popular measures like [[IR Evaluation Measures|DCG]] and [[IR Evaluation Measures|ERR]] are found to be neither ordinal nor interval scales in multi-graded settings, raising questions about the validity of current IR evaluation practices.

## Academic Debate
There is an ongoing debate ([[Norbert Fuhr]] vs. [[Tetsuya Sakai]]) regarding whether the community should strictly avoid averaging non-interval scales or if such practices are acceptable given their alignment with user intuition and practices in other fields.

## Conclusion
Understanding [[Measurement Scales]] is not just a theoretical exercise but a practical necessity for ensuring the reliability and interpretability of experimental results in Search Engine evaluation.
