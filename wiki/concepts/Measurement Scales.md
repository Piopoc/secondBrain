# Measurement Scales

Measurement scales are used to categorize the type of numerical assignment given to an attribute, which in turn determines the valid mathematical and statistical operations that can be performed on the data.

## Stevens' Classification (1946)

S. S. Stevens identified four primary types of measurement scales:

### 1. Nominal Scale
The most basic scale where numerals serve only as **labels or type numbers**.
- **Operation:** Determination of equality.
- **Invariance:** Permutation group (any one-to-one substitution).
- **Permissible Statistics:** Mode, Contingency correlation.
- **Example:** Numbering of football players, classification of document types.

### 2. Ordinal Scale
Numerals indicate a relative position or order.
- **Operation:** Determination of "greater than" or "less than".
- **Invariance:** Isotonic group (any monotonic increasing function).
- **Permissible Statistics:** Median, Percentiles.
- **Example:** Rank of a document in a search result list.

### 3. Interval Scale
Numerals represent equal intervals between values, but there is no meaningful absolute zero.
- **Operation:** Determination of equality of intervals or differences.
- **Invariance:** General linear group (affine transformations: $m' = am + b$).
- **Permissible Statistics:** Mean, Standard deviation, Rank-order correlation, Product-moment correlation.
- **Example:** Temperature in Celsius or Fahrenheit.

### 4. Ratio Scale
The most restrictive scale, featuring a meaningful absolute zero and equal ratios.
- **Operation:** Determination of equality of ratios.
- **Invariance:** Similarity group (multiplication by a constant: $m' = am$).
- **Permissible Statistics:** Coefficient of variation.
- **Example:** Height, weight, or duration.

## Cumulative Nature
The requirements for these scales are cumulative:
- To have an **Ordinal** scale, you must first be able to determine equality (Nominal).
- To have an **Interval** scale, you must first be able to determine order (Ordinal).
- To have a **Ratio** scale, you must first be able to determine equal intervals (Interval).

## Relevance to IR
In Information Retrieval, understanding the scale type is crucial for choosing the correct statistical test (e.g., using a Sign Test for ordinal data vs. a t-test for interval data). Applying a test that assumes a higher scale than what the measure provides can lead to **meaningless** results.
