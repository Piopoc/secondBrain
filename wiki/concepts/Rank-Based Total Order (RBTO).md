# Rank-Based Total Order (RBTO)

**Rank-Based Total Order (RBTO)** is an interval scale measure for IR based on the principle of **strong top-heaviness**.

## The Principle of Strong Top-Heaviness
Under this principle, any single relevant document ranked higher is preferred over any number of relevant documents ranked below it. This mirrors a user's preference for finding the most relevant information as early as possible.

## Definition
The rank function $\rho(\hat{r})$ for RBTO is defined as:
$$\text{RBTO}(\hat{r}) = \sum_i 2^{N-i} \times \hat{r}[i]$$
This is essentially a binary representation of the relevance string, where the position $i$ has a weight of $2^{N-i}$.

## Relation to Rank-Based Measures
Unlike set-based measures, most rank-based measures are **not** interval scales except under very specific conditions:

- **Rank-Biased Precision (RBP):**
  - If $p = 0.5$, RBP is an interval scale because $\text{RBP}(\hat{r}) = \frac{1}{2^N} \times \text{RBTO}(\hat{r})$.
  - If $p < 0.5$, RBP is only an **ordinal scale**.
  - If $p > 0.5$, RBP is ordinal with respect to a different order.
- **Average Precision (AP):** AP is not even an ordinal scale with respect to strong top-heaviness.

## Summary of Findings
The fact that common measures like AP or RBP (with $p \neq 0.5$) are only ordinal (or not even ordinal) suggests that using them in statistical tests that assume interval data (like t-tests) may produce meaningless results.
