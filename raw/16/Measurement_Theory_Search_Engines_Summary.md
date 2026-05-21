# Measurement, Scales, Averages, Meaningfulness — Search Engines (A.Y. 2025/2026)

## Detailed Summary of: *16-se-2025-26-measurement-theory_compressed.pdf*

**Course:** Search Engines  
**Degrees:** Master in Computer Engineering, Master in Data Science  
**Academic Year:** 2025/2026  
**Author:** Nicola Ferro — Intelligent Interactive Information Access (IIIA) Hub, Department of Information Engineering, University of Padua  
**Joint Work with:** Eleonora Losiouk, Maria Maistro, Silvia Pontarollo, Marco Ferrante, Norbert Fuhr

---

## Table of Contents

1. [The Problem](#1-the-problem)
2. [Measurement Scales](#2-measurement-scales)
3. [Temperature: An Interval Scale Example](#3-temperature-an-interval-scale-example)
4. [Meaningfulness](#4-meaningfulness)
5. [IR Measures We Are Talking About](#5-ir-measures-we-are-talking-about)
6. [Why Care About Measurement Issues in IR](#6-why-care-about-measurement-issues-in-ir)
7. [The Representational Measurement Theory](#7-the-representational-measurement-theory)
8. [Measurement Issues in IR](#8-measurement-issues-in-ir)
9. [A General Theory of IR Measures](#9-a-general-theory-of-ir-measures)
10. [Experiments](#10-experiments)
11. [A Debated Issue](#11-a-debated-issue)
12. [Lessons Learnt](#12-lessons-learnt)
13. [Going Multi-Graded](#13-going-multi-graded)

---

## 1. The Problem

Information Retrieval (IR) experimentation is deeply rooted in the evaluation of system performance, but the field faces fundamental questions about the nature of its measurements. IR relies on measures such as Precision, Recall, Average Precision (AP), Discounted Cumulative Gain (DCG), Rank-Biased Precision (RBP), and Reciprocal Rank (RR) to quantify how well a retrieval system performs. However, a critical question arises: **what kind of measurement scales do these measures actually constitute?**

This is not merely a theoretical concern. The type of scale a measure belongs to determines what mathematical and statistical operations are valid. For instance, computing an arithmetic mean is only meaningful on an interval scale, while computing a median is valid on an ordinal scale. If we apply statistical operations that are not appropriate for the scale type, the resulting statements may be meaningless — not wrong in the sense of being false, but meaningless in the sense that their truth or falsity is not preserved under the permissible transformations of the underlying scale.

The lecture addresses these concerns by grounding IR evaluation in the **representational theory of measurement**, providing a rigorous framework for understanding the scale properties of IR measures, and investigating the consequences of violating measurement-theoretic assumptions.

---

## 2. Measurement Scales

### 2.1 Stevens' Classification of Measurement Scales

The foundational classification of measurement scales was proposed by S. S. Stevens in his seminal 1946 paper *"On the Theory of Scales of Measurement"* (Science, Vol. 103, No. 2684). Stevens identified four types of scales, each characterized by the basic empirical operations needed to create them, the mathematical group structure that preserves the scale form, and the permissible statistics:

| Scale | Basic Empirical Operations | Mathematical Group Structure | Permissible Statistics |
|-------|---------------------------|------------------------------|----------------------|
| **Nominal** | Determination of equality | Permutation group: m' = f(m), where f means any one-to-one substitution | Mode, Contingency correlation |
| **Ordinal** | Determination of greater or less | Isotonic group: m' = f(m), where f means any monotonic increasing function | Median, Percentiles |
| **Interval** | Determination of equality of intervals or differences | General linear group: m' = am + b | Mean, Standard deviation, Rank-order correlation, Product-moment correlation |
| **Ratio** | Determination of equality of ratios | Similarity group: m' = am | Coefficient of variation |

### 2.2 Nominal Scale

The nominal scale represents the most unrestricted assignment of numerals. The numerals are used only as **labels or type numbers**, and words or letters would serve equally well. Two types of nominal assignments are sometimes distinguished: (a) the "numbering" of football players for the identification of individuals, and (b) the "numbering" of types or classes, where each member of a class is assigned the same numeral. Since the purpose is just as well served when any two designating numerals are interchanged, this scale form remains invariant under the general substitution or permutation group. The only statistic relevant to nominal scales is the number of cases.

### 2.3 Ordinal Scale

The ordinal scale requires the ability to determine whether one entity is greater or less than another. The scale form remains invariant under any **monotonic increasing transformation** — that is, any transformation that preserves the order. The median (mid-point) of a distribution maintains its position under all transformations that preserve order (isotonic group). Permissible statistics include the median and percentiles.

### 2.4 Interval Scale

The interval scale requires the ability to determine **equality of intervals or differences**. It remains invariant under the general linear group of transformations: m' = am + b (affine transformations). An item located at the mean remains at the mean only under transformations as restricted as those of the linear group. Permissible statistics include the mean, standard deviation, rank-order correlation, and product-moment correlation.

### 2.5 Ratio Scale

The ratio scale requires the ability to determine **equality of ratios**. It remains invariant only under the similarity transformation (multiplication by a constant): m' = am. The coefficient of variation remains invariant only under this transformation. This is the most restrictive scale type, requiring a meaningful zero point.

### 2.6 Cumulative Nature of Scales

The column listing the basic operations needed to create each type of scale is **cumulative**: to an operation listed opposite a particular scale must be added all those operations preceding it. Thus, an interval scale can be erected only provided we have an operation for determining equality of intervals, for determining greater or less, and for determining equality (not greater and not less). To these operations must be added a method for ascertaining equality of ratios if a ratio scale is to be achieved.

---

## 3. Temperature: An Interval Scale Example

Temperature provides an excellent concrete illustration of how interval scales work and what operations are and are not permissible:

### 3.1 Multiplication and Division Are Not Allowed

20°C is **not** twice as hot as 10°C. Division is not invariant with respect to the transformation F = C × (9/5) + 32:

- In Celsius: 20 / 10 = 2
- In Fahrenheit: 68 / 50 = 1.36

Since the ratio changes under the permissible affine transformation, the statement "20°C is twice as hot as 10°C" is **not meaningful** on an interval scale.

### 3.2 Addition and Subtraction Are Allowed

The increase between 10°C and 20°C is the same as the increase between 20°C and 30°C. Subtraction is invariant with respect to the transformation:

- In Celsius: 30 - 20 = 20 - 10 = 10
- In Fahrenheit: 86 - 68 = 68 - 50 = 18

The differences are consistent (both equal in their respective scales).

### 3.3 Ratio of Intervals Is Invariant

The ratio of intervals is also invariant with respect to the transformation:

- In Celsius: (20 - 10) / (30 - 20) = 1
- In Fahrenheit: (68 - 50) / (86 - 68) = 1

---

## 4. Meaningfulness

### 4.1 Definition

Statistical operations on measurements of a given scale are **not appropriate or inappropriate per se** but only relative to the kinds of statements made about them. The criterion of appropriateness for a statement about a statistical operation is that the statement be **empirically meaningful** in the sense that its truth or falsity must be **invariant under permissible transformations** of the underlying scale.

Meaningfulness is a **distinct concept from the truth** of a statement and is somehow close to the notion of **invariance** in geometry. A statement can be true but meaningless (in the measurement-theoretic sense), or meaningful but false.

*References:*
- Adams, E. W., Fagot, R. F., and Robinson, R. E. (1965). *A theory of appropriate statistics.* Psychometrika, 30:99–127.
- Narens, L. (2002). *Theories of Meaningfulness.* Lawrence Erlbaum Associates.

### 4.2 Temperature: Meaningfulness Examples

Consider temperature readings in Paris (P) and Rome (R):

**In Celsius:** P = [2, 2, 4, 8, 36], R = [1, 2, 4, 15, 34]  
**In Fahrenheit:** P = [35.6, 35.6, 39.2, 46.4, 96.8], R = [33.8, 35.6, 39.2, 59.0, 93.2]

- **"The median temperature in Paris is the same as in Rome"** — **Meaningful.** The median is 4 in both Celsius and 39.2 in both Fahrenheit. Interval scales are also ordinal, and quantiles are an allowable operation on ordinal scales.

- **"The mean temperature in Paris is less than in Rome"** — **Meaningful.** 10.4 < 11.2 in Celsius and 50.72 < 52.16 in Fahrenheit. Addition and subtraction are allowable operations on an interval scale, and the mean is invariant to affine transformations.

- **"The geometric mean of temperature in Paris is greater than in Rome"** — **Not meaningful.** 5.40 > 5.27 in Celsius but 46.74 < 48.17 in Fahrenheit. The geometric mean involves multiplication and division of values, which is not a permitted operation on an interval scale, so the truth of the statement changes under a permissible transformation.

---

## 5. IR Measures We Are Talking About

The lecture focuses on the following IR evaluation measures, presenting their mathematical formulations:

- **Precision (P):** The proportion of retrieved documents that are relevant.
- **Recall (R):** The proportion of relevant documents that are retrieved, dependent on the Recall Base (RB).
- **F-measure (F):** The harmonic mean of Precision and Recall.
- **Average Precision (AP):** The arithmetic mean of the precision values at the positions of relevant documents, also dependent on the Recall Base.
- **Discounted Cumulative Gain (DCG):** A measure that incorporates the relevance degree of each document, with a discount factor based on rank position and a document cut-off value b.
- **Rank-Biased Precision (RBP):** Models user patience with a persistence parameter p; the probability that the user visits the next rank position is p.
- **Reciprocal Rank (RR):** The reciprocal of the rank position of the first relevant document.

Each of these measures can be visualized in the Precision-Recall space, and they exhibit different properties depending on the scale type they belong to.

---

## 6. Why Care About Measurement Issues in IR

Understanding the scale type of IR measures has direct practical consequences for **statistical significance testing**. The choice of appropriate statistical test depends on the scale of measurement:

| Task/Concern | Appropriate Statistical Test | Required Scale |
|---|---|---|
| Comparing system performance | Sign Test | Ordinal scale |
| Topic difficulty and robust retrieval | Wilcoxon Rank Sum Test | Ordinal scale |
| Score transformation and standardization techniques | Wilcoxon Signed Rank Test | Interval scale |
| Cost function in Machine Learning | Student's t Test | Interval scale |
| Query Performance Prediction | ANOVA | Interval scale |
| | Kruskal-Wallis Test | Ordinal scale |
| | Friedman Test | Ordinal scale |

Using a statistical test that requires a higher scale type than the measure actually provides (e.g., applying a t-test to an ordinal measure) may produce **meaningless results** — statements whose truth is not preserved under permissible transformations.

---

## 7. The Representational Measurement Theory

### 7.1 Core Concepts

The representational theory of measurement provides the formal foundation for understanding measurement scales. It is based on the following principles:

1. **Empirical relations:** There exists an empirical relation which orders entities on the basis of their attributes. For example, you can compare two rods and determine which is longer or whether they are equal.

2. **Concatenation:** The empirical relation may support concatenation. For example, the concatenation of a rod with another one is longer than both of them.

3. **Homomorphism:** There exists a homomorphism φ (the measurement scale) which maps entities into numbers and the empirical relation into a numerical relation which preserves the ordering (and concatenation):
   - e₁ ≾ e₂ ⇔ φ(e₁) ≤ φ(e₂)
   - φ(e₁ ∘ e₂) = φ(e₁) + φ(e₂)

This formalism is grounded in the work of Krantz, Luce, Suppes, and Tversky (1971) and Fenton and Bieman (2014).

### 7.2 From Theory to Practice: An Example with Trees

The lecture uses a practical example with three trees (Papaya, Banana, Ananas) of different heights to illustrate the theory:

- Papaya Tree taller than Banana Tree → φ(Papaya) > φ(Banana)
- Papaya Tree taller than Ananas Tree → φ(Papaya) > φ(Ananas)
- Banana Tree taller than Ananas Tree → φ(Banana) > φ(Ananas)
- "Much taller" relations correspond to numerical differences exceeding a threshold (e.g., φ(Papaya) > φ(Ananas) + 50)

### 7.3 Difference Structures and Interval Scales

A **difference structure** is a formal construct that enables the creation of an interval scale. It is defined as a finite (non-empty) set of objects A carrying a property x, with a binary relation ≾_d on A × A satisfying four axioms:

1. **≾_d is a weak order** — there is an order on intervals.
2. **If Δ_ab ≾_d Δ_cd, then Δ_dc ≾_d Δ_ba** — refers to sign differences.
3. **If Δ_ab ≾_d Δ_a'b' and Δ_bc ≾_d Δ_b'c', then Δ_ac ≾_d Δ_a'c'** — weak monotonicity, the basic concatenation rule for intervals.
4. **If Δ_ab ≾_d Δ_cd ≺_d Δ_a'b', then there exist d', d'' such that Δ_ad' ~ Δ_cd and Δ_d''b ~ Δ_a'd** — the solvability condition, ensuring that whenever we have two non-equivalent intervals, we can always find intermediate elements.

**Representation Theorem:** If (A, ≾_d) is a difference structure, then there exists a function m: A → ℝ (a measure function) such that, for each a, b, c, d ∈ A: Δ_ab ≾_d Δ_cd ⇔ m(a) - m(b) ≥ m(c) - m(d).

**Uniqueness Theorem:** Any other measure function m* is such that m*(a) = αm(a) + β, with α > 0 — the interval scale is unique up to affine (positive linear) transformations.

---

## 8. Measurement Issues in IR

### 8.1 The Core Problem: No Empirical Ordering

As C. J. "Keith" van Rijsbergen noted in 1981:

> *"In the physical sciences there is usually an empirical ordering of the quantities we wish to measure [...] Such a situation does not hold for information retrieval. There is no empirical ordering for retrieval effectiveness and therefore any measure of retrieval effectiveness will by necessity be artificial."*

This fundamental observation highlights that IR measures lack the natural empirical ordering found in physical measurements (like length or weight), making it particularly challenging to establish their scale properties.

### 8.2 Ordering Problem

Given different retrieval runs (combinations of relevant and non-relevant documents at various ranks), it is not always clear how to establish a consistent ordering among them. Some runs are clearly better than others, but many pairs of runs are **incomparable** — there is no natural way to determine which is better.

### 8.3 Interval Problem

To determine whether a measure is interval-based, we need:
- A notion of **interval** among runs
- A notion of **length** of an interval among runs

This raises questions such as: Which runs fall in-between two given runs? How many intermediate levels exist between a "highly relevant" run and a "not relevant" run? These questions do not have straightforward answers in IR.

### 8.4 Transformation Problem

The Stevens classification shows that each scale type has specific permissible transformations. The question is: under which transformations do IR measures preserve their meaning? If an IR measure is only on an ordinal scale, then any monotonic transformation is permissible, which severely limits the valid statistical operations.

### 8.5 Galileo's Inspiration

Despite these challenges, the lecture invokes Galileo Galilei's famous quote as motivation:

> *"Measure what is measurable and make measurable what is not"*

This encourages the IR community to not give up on measurement issues, but rather to develop rigorous theoretical frameworks for understanding and improving IR evaluation measures.

---

## 9. A General Theory of IR Measures

### 9.1 Approach

The lecture presents a general theory of IR measures grounded in the representational theory of measurement. The approach proceeds as follows:

1. **Define orders and intervals among runs** — This leads to partially ordered sets (posets).
2. **Introduce a proper structure among runs** — Using orders and intervals, define a structure that allows us to construct an interval scale measure by construction.
3. **Transform IR measures to the interval scale** — Try to transform existing IR measures to the interval scale and determine whether they are interval scales or not.

### 9.2 Key Findings

- **SBTO (Set-Based Total Order)** and **RBTO (Rank-Based Total Order)** are two interval scale measures formally derived from the theory.
- **Set-based measures are interval scales** — Precision, Recall, and F-measure are transformations of SBTO (with some caveats related to the recall base).
- **Rank-based measures are interval scales only under very strict conditions**, hardly met in practice:
  - RBP with p = 0.5 is interval (it is a transformation of RBTO).
  - RBP with p < 0.5 is ordinal.
  - RBP with p > 0.5 is ordinal with respect to a different order.
- **When going multi-graded (using graded relevance), the situation becomes even more challenging.**

*Reference:* Ferrante, M., Ferro, N., and Pontarollo, S. (2019). *A General Theory of IR Evaluation Measures.* IEEE TKDE, 31(3):409–422.

### 9.3 Set-Based Total Order (SBTO)

Runs are ordered by their total mass of relevance. The unique rank function is ρ(r̂) = Σᵢ r̂ᵢ, which together with the natural distance induces a difference structure. The interval scale is:

**SBTO(r̂) = ρ(r̂) = Σᵢ r̂ᵢ**

Traditional set-based measures are all interval scales because they are affine transformations of SBTO:
- **Precision:** P(r̂) = (1/N) × SBTO(r̂)
- **Recall:** R(r̂) = (1/RB) × SBTO(r̂)
- **F-measure:** F(r̂) = 2 / (N + RB) × SBTO(r̂)

### 9.4 Rank-Based Total Order (RBTO)

Under **strong top-heaviness**, runs are ordered by the principle that any single relevant document ranked higher is preferred to any number of relevant documents ranked just below it. The unique rank function is ρ(r̂) = Σᵢ 2^(N-i) × r̂[i], which is essentially the base-10 representation of the binary string. The interval scale is:

**RBTO(r̂) = Σᵢ 2^(N-i) × r̂[i]**

Key findings for rank-based measures:
- RBP with p = 1/2 is an interval scale: RBP(r̂) = (1/2^N) × RBTO(r̂)
- RBP with p < 1/2 is ordinal
- RBP with p > 1/2 is not even ordinal with respect to strong top-heaviness
- AP is not even ordinal with respect to strong top-heaviness

---

## 10. Experiments

### 10.1 Experimental Setup

The experimental analysis investigates how IR measures relate to their ranked (ordinal) versions using Kendall's τ correlation. The key question is: **how much does a measure's ordering differ from a purely ordinal ranking?** A high correlation means the measure is close to an interval scale; a low correlation means it departs significantly from intervalness.

### 10.2 Key Results

- **Precision and RBP (p = 0.5)** show perfect Kendall's τ = 1.000, indicating they are interval scales (consistent with the theoretical findings).
- **DCG** measures show very high correlations (0.91–1.000), suggesting they are close to interval scales.
- **Reciprocal Rank (RR)** shows the lowest correlations (0.67–0.93), systematically lower than all other measures. This indicates that transforming RR into an interval scale requires a more marked correction — it experiences a drop in "intervalness" of 7–33%.
- **RR departs more and more from the interval scale assumption as the run length increases.** This is because as the run gets longer, the step function of RR becomes increasingly non-linear with respect to the interval scale.
- **nDCG** generally shows high correlations, close to 1.000 in many configurations.

### 10.3 Impact on Statistical Testing

The experimental results confirm that the scale type of a measure has a **sizeable impact** on both correlation analysis and statistical significance testing. Using measures that are only ordinal in tests that assume interval data (e.g., t-tests, ANOVA) may produce misleading results, while using appropriate non-parametric tests (e.g., sign test, Wilcoxon) for ordinal data preserves meaningfulness.

---

## 11. A Debated Issue

### 11.1 Fuhr's Position (2017)

Norbert Fuhr, in his 2017 SIGIR Forum paper *"Some Common Mistakes in IR Evaluation, And How They Can Be Avoided"*, argued that the community should **not**:
- Use RR or AP
- Average measures that are not on an interval scale

His argument is rooted in measurement theory: if a measure is not on an interval scale, computing arithmetic means over it is not meaningful, since the mean is not invariant under the permissible transformations of ordinal scales.

### 11.2 Sakai's Response (2020)

Tetsuya Sakai, in his 2020 SIGIR Forum paper *"On Fuhr's Guideline for IR Evaluation"*, pushed back against Fuhr's prescriptive approach, arguing that:
- One shouldn't be prescriptive towards the community
- Other communities average ordinal measures anyway
- RR is close to user behavior and our intuition

### 11.3 Ferro, Ferro, and Fuhr's Response (2022)

The authors' response (2022, arXiv:2212.11735) takes a nuanced position:
- **IR measures are a valid numerical mapping of an ordinal scale**, thus they constitute a non-equispaced interval scale, and therefore you **can** average them.
- You **can** make meaningful statements using RR.
- They are not convinced about using the ranked version of a measure.
- Theoretical definitions require equi-spacing for an interval scale (to the best of their knowledge).
- **Meaningfulness is intended in a different technical sense** than what some critics assume.
- As a community, **we should discuss and investigate better** rather than reduce everything to a binary contrast (average or not, RR or not). We may risk losing an opportunity for improvement.

### 11.4 Moffat's Comment (2022)

Alistair Moffat, in his 2022 IEEE Access paper *"Batch Evaluation Metrics in Information Retrieval: Measures, Scales, and Meaning"*, contributed further perspectives to this ongoing debate, emphasizing the importance of understanding what scale type each measure belongs to.

---

## 12. Lessons Learnt

### 12.1 Key Takeaways

1. **It is possible to develop a theory of IR measures** grounded in the representational theory of measurement. This provides a rigorous, formal foundation rather than relying on intuition or convention.

2. **We determined the scale properties of several state-of-the-art IR measures.** There are issues with intervalness, but even more with the recall base and run length — these factors significantly affect the scale type of a measure.

3. **Experimental results agree with the expected properties of the measures.** You need to "deep dive" to really understand the behavior of each measure. The theoretical predictions about which measures are interval scales and which are ordinal are borne out by empirical correlation analyses.

4. **There is a sizeable impact on both correlation analysis and statistical significance testing.** The scale type of a measure directly affects which statistical tests are appropriate and which statements about system comparisons are meaningful.

### 12.2 Open Questions

- **We may need to rethink how we use our analytical tools** and how we explain and understand their outcomes.
- **How/whether the validity of our experiments may be impacted** is still an open question.
- **Meaningfulness should be a central concern in IR** — not just an academic exercise, but a practical consideration that affects the reliability and interpretability of experimental results.

---

## 13. Going Multi-Graded

### 13.1 The Challenge

When moving from binary relevance (relevant/not relevant) to **multi-graded relevance** (where documents can have different degrees of relevance, e.g., 0, 1, 2, ..., c), the measurement-theoretic analysis becomes significantly more complex.

### 13.2 Multi-Graded Set-Based Measures

The interval scale for multi-graded set-based measures becomes:

**SBTO(r̂) = Σᵢ (𝟙(r̂ᵢ) × Nⁱ) / (i + 1)**

where 𝟙(·) is the indicator function of the relevance degree.

This can become **computationally challenging** as the number of relevance grades increases.

### 13.3 Multi-Graded Rank-Based Measures

The interval scale for multi-graded rank-based measures is:

**RBTO(r̂) = Σᵢ 𝟙(r̂[i]) × (c + 1)^(N-i)**

A key observation is that the binomial coefficient decreases as we retrieve documents with the same relevance degree more than once, introducing a **dynamic notion of relevance** that complicates the analysis.

### 13.4 Multi-Graded Findings

- **Set-based measures:** Generalised Precision (gP) and generalised Recall (gR) are **neither ordinal nor interval scales** in the multi-graded case.
- **Rank-based measures:**
  - gRBP with p ≤ G/(G+1) is an **ordinal scale** (where G is the normalized smallest gap between the gain of two consecutive relevance degrees).
  - gRBP with p = G/(G+1) is an **interval scale**, but only if the relevance degrees are on a **ratio scale** — a very strong requirement.
  - gRBP with p > G/(G+1), DCG, and ERR are **neither ordinal nor interval scales**.

### 13.5 Implications

The multi-graded findings are particularly significant because many modern IR evaluation campaigns (such as TREC) use graded relevance assessments. The fact that popular measures like DCG and ERR are not interval scales (and in some cases not even ordinal scales) in the multi-graded setting raises serious questions about the validity of the statistical analyses commonly performed in IR evaluation. This suggests that the community needs to develop new measures or new analytical frameworks that properly account for the scale properties of evaluation metrics in multi-graded relevance scenarios.
