# 📝 IR Exam Simulation: Numerical Exercises

This document contains simulated exercises for the Information Retrieval partial exam. Each exercise is designed to be solved with a calculator in 15-20 minutes.

## 🎯 Exam Strategy
- **Time**: 1 hour for 4-5 questions.
- **Numerical Question**: Expect one exercise involving TF-IDF, Evaluation Metrics, or Probabilistic Models.
- **Key**: Always write the formula first, then substitute the values.

---

## 🛠️ Exercise 1: TF-IDF and Cosine Similarity
**Scenario**: You have a small corpus of 3 documents and a query $q$.
- **Corpus**:
	- $D_1$: "il gatto mangia il pesce"
	- $D_2$: "il cane mangia l'osso"
	- $D_3$: "il gatto dorme sul divano"
- **Query**: $q$: "gatto mangia"

**Task**:
1. Compute the **TF-IDF** weights for the terms in the query for $D_1$ and $D_2$.
2. Calculate the **Cosine Similarity** between $q$ and $D_1$.

**Assume**:
- Use **Relative TF**: $tf_{i,k} = \frac{f_{i,k}}{\sum f_{j,k}}$
- Use **Standard IDF**: $idf_i = \log_{10} \frac{N}{n_i}$
- Stopwords (il, l', sul) are removed.

### 🗝️ Solution Sketch
1. **Preprocessing**:
	- $D_1$: {gatto: 1, mangia: 1, pesce: 1} (Total: 3)
	- $D_2$: {cane: 1, mangia: 1, osso: 1} (Total: 3)
	- $D_3$: {gatto: 1, dorme: 1, divano: 1} (Total: 3)
	- $q$: {gatto: 1, mangia: 1} (Total: 2)
2. **IDF Calculation**:
	- $idf(\text{gatto}) = \log_{10}(3/2) \approx 0.176$
	- $idf(\text{mangia}) = \log_{10}(3/2) \approx 0.176$
3. **Weights for $D_1$**:
	- $w(\text{gatto}, D_1) = (1/3) \cdot 0.176 = 0.058$
	- $w(\text{mangia}, D_1) = (1/3) \cdot 0.176 = 0.058$
4. **Cosine Similarity**:
	- $\vec{q} = [w(\text{gatto}, q), w(\text{mangia}, q)]$ (Note: query IDF is usually not used or handled differently, but if using the same IDF: $[(1/2 \cdot 0.176), (1/2 \cdot 0.176)]$)
	- $\vec{D_1} = [0.058, 0.058, w(\text{pesce}, D_1)]$
	- $\text{sim}(q, D_1) = \frac{(0.088 \cdot 0.058) + (0.088 \cdot 0.058)}{\sqrt{0.088^2 + 0.088^2} \cdot \sqrt{0.058^2 + 0.058^2 + w(\text{pesce})^2}}$

---

## 📈 Exercise 2: Evaluation Metrics (The "Classic")
**Scenario**: A system retrieves 10 documents for a topic. The **Recall Base (RB)** for this topic is **4**.
The relevance judgments (Ground Truth) are:
- Relevant docs: $\{D_2, D_5, D_8, D_{12}\}$
- System Ranking: $D_1, D_2, D_3, D_5, D_6, D_7, D_8, D_9, D_{10}, D_{11}$

**Task**:
1. Calculate **Precision at 5 (P@5)**.
2. Calculate **Recall at 5 (R@5)**.
3. Calculate the **Average Precision (AP)** for this query.

### 🗝️ Solution Sketch
1. **P@5**:
	- Top 5: $\{D_1, D_2, D_3, D_5, D_6\}$
	- Relevant in Top 5: $\{D_2, D_5\}$ (Count = 2)
	- $P@5 = 2/5 = 0.4$ (40%)
2. **R@5**:
	- Relevant in Top 5: 2
	- Total Relevant (RB): 4
	- $R@5 = 2/4 = 0.5$ (50%)
3. **AP**:
	- Precision at rank 2 (first rel): $1/2 = 0.5$
	- Precision at rank 4 (second rel): $2/4 = 0.5$
	- Precision at rank 7 (third rel): $3/7 \approx 0.428$
	- Fourth rel is $D_{12}$ (not in top 10) $\rightarrow$ Precision = 0.
	- $AP = \frac{0.5 + 0.5 + 0.428 + 0}{4} = \frac{1.428}{4} = 0.357$

---

## 🧮 Exercise 3: BM25 Score
**Scenario**: Calculate the score of a document $d$ for a query containing a single term $t$.
- $f(t, d) = 3$ (Term $t$ appears 3 times in $d$)
- $|d| = 100$ words
- $\text{avgdl} = 80$ words
- $idf(t) = 2.5$
- Parameters: $k_1 = 1.2, b = 0.75$

**Task**: Compute the BM25 score.

### 🗝️ Solution Sketch
Formula: $\text{score} = idf(t) \cdot \frac{f(t, d) \cdot (k_1 + 1)}{f(t, d) + k_1 \cdot (1 - b + b \cdot \frac{|d|}{\text{avgdl}})}$
1. **Denominator part**:
	- $1 - 0.75 + 0.75 \cdot (100/80) = 0.25 + 0.75 \cdot 1.25 = 0.25 + 0.9375 = 1.1875$
2. **Full Denominator**:
	- $3 + 1.2 \cdot 1.1875 = 3 + 1.425 = 4.425$
3. **Numerator**:
	- $2.5 \cdot (3 \cdot 2.2) = 2.5 \cdot 6.6 = 16.5$
4. **Final Score**:
	- $16.5 / 4.425 \approx 3.728$

---

## ☁️ Exercise 4: Language Model Smoothing
**Scenario**:
- Document $D$ contains 100 words.
- Term $t$ appears 2 times in $D$.
- In the whole collection $C$ of $10^6$ words, term $t$ appears 500 times.
- Smoothing parameter $\lambda = 0.1$ (Jelinek-Mercer).

**Task**: Calculate the smoothed probability $P(t | D)$.

### 🗝️ Solution Sketch
Formula: $P(t | D) = (1-\lambda) \frac{f_{t,D}}{|D|} + \lambda \frac{f_{t,C}}{|C|}$
1. **Doc Prob**: $2/100 = 0.02$
2. **Coll Prob**: $500 / 1,000,000 = 0.0005$
3. **Weighted Sum**:
	- $P = (0.9 \cdot 0.02) + (0.1 \cdot 0.0005)$
	- $P = 0.018 + 0.00005 = 0.01805$

---

## 🔄 Exercise 5: Rocchio Algorithm (Relevance Feedback)
**Scenario**: You are using a Vector Space Model with 3 dimensions.
- **Initial Query**: $\vec{q} = [1, 0, 1]$
- **Relevant Documents (Rel)**: 
	- $\vec{d_1} = [2, 1, 0]$
	- $\vec{d_2} = [1, 2, 1]$
- **Non-Relevant Documents (NotRel)**:
	- $\vec{d_3} = [0, 0, 2]$
- **Parameters**: $\alpha = 1, \beta = 0.75, \gamma = 0.25$

**Task**: Compute the updated query vector $\vec{q}'$.

### 🗝️ Solution Sketch
Formula: $\vec{q}' = \alpha \vec{q} + \beta \frac{1}{|\text{Rel}|} \sum_{d \in \text{Rel}} \vec{d} - \gamma \frac{1}{|\text{NotRel}|} \sum_{d \in \text{NotRel}} \vec{d}$

1. **Centroid of Relevant Docs**:
	- $\text{Centroid}_{\text{Rel}} = \frac{1}{2} ([2, 1, 0] + [1, 2, 1]) = [1.5, 1.5, 0.5]$
2. **Centroid of Non-Relevant Docs**:
	- $\text{Centroid}_{\text{NotRel}} = \frac{1}{1} ([0, 0, 2]) = [0, 0, 2]$
3. **Weighted Sum**:
	- $\vec{q}' = 1 \cdot [1, 0, 1] + 0.75 \cdot [1.5, 1.5, 0.5] - 0.25 \cdot [0, 0, 2]$
	- $\vec{q}' = [1, 0, 1] + [1.125, 1.125, 0.375] - [0, 0, 0.5]$
4. **Final Result**:
	- $\vec{q}' = [2.125, 1.125, 0.875]$

