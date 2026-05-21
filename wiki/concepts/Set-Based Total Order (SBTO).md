# Set-Based Total Order (SBTO)

**Set-Based Total Order (SBTO)** is an interval scale measure derived from the representational theory of measurement, specifically designed for set-based IR evaluation.

## Definition
SBTO orders retrieval runs based on their **total mass of relevance**. The rank function $\rho(\hat{r})$ is defined as the sum of relevance of all retrieved documents:
$$\text{SBTO}(\hat{r}) = \rho(\hat{r}) = \sum_i \hat{r}_i$$

## Relation to Traditional Measures
Many traditional set-based IR measures are actually affine transformations of SBTO, which makes them **interval scales**:

- **Precision (P):** $P(\hat{r}) = \frac{1}{N} \times \text{SBTO}(\hat{r})$
- **Recall (R):** $R(\hat{r}) = \frac{1}{RB} \times \text{SBTO}(\hat{r})$ (where $RB$ is the Recall Base)
- **F-measure (F):** $F(\hat{r}) = \frac{2}{N + RB} \times \text{SBTO}(\hat{r})$

## Key Implications
Because these measures are transformations of SBTO, they satisfy the requirements of an interval scale. This means that statistical operations like computing the **arithmetic mean** are empirically meaningful for these measures.
