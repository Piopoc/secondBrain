# Rocchio Algorithm

The **Rocchio Algorithm** is the classic method for implementing **Relevance Feedback (RF)** in Information Retrieval. It is based on the assumption that relevant documents are more similar to each other than they are to non-relevant documents.

## 🎯 Core Intuition
The algorithm treats the query as a vector in the [[concepts/Vector-Space-Model]]. The goal is to iteratively refine the query vector $\vec{q}$ by moving it:
1. **Towards** the centroid (average) of the documents marked as **relevant**.
2. **Away** from the centroid of the documents marked as **non-relevant**.

## 🧮 The Mathematical Formula
The updated query vector $\vec{q}'$ is calculated as:

$$\vec{q}' = \alpha \vec{q} + \beta \frac{1}{|\text{Rel}|} \sum_{d \in \text{Rel}} \vec{d} - \gamma \frac{1}{|\text{NotRel}|} \sum_{d \in \text{NotRel}} \vec{d}$$

### Parameter Breakdown
- $\alpha$ (**Original Intent**): Controls how much of the original query is preserved. A high $\alpha$ prevents the query from drifting too far from the user's initial search.
- $\beta$ (**Positive Feedback**): Controls the influence of relevant documents. It "pulls" the query vector toward the cluster of documents the user liked.
- $\gamma$ (**Negative Feedback**): Controls the influence of non-relevant documents. It "pushes" the query vector away from the cluster of documents the user rejected.

## 🔄 The Iterative Process
1. **Initial Search**: The user submits $\vec{q}$ and the system returns a ranked list.
2. **Feedback**: The user marks a subset of results as **Relevant (Rel)** and another as **Non-Relevant (NotRel)**.
3. **Update**: The system applies the Rocchio formula to compute $\vec{q}'$.
4. **Re-search**: The system performs a new search using $\vec{q}'$, which should now be more aligned with the user's actual information need.

## 🤖 Pseudo-Relevance Feedback (PRF)
Since manual feedback is tedious for users, **PRF** automates the process:
- **Assumption**: The system assumes that the top $K$ documents in the initial ranking are all relevant ($\text{Rel} = \text{top-K}$, $\text{NotRel} = \emptyset$).
- **Mechanism**: It automatically updates the query using only the $\beta$ term.
- **Benefit**: Significant boost in recall and precision without user intervention.

## ⚠️ Critical Risks
### 1. Query Drifting
This occurs when the initial results are poor. In PRF, if the top-K documents are actually irrelevant, the algorithm will pull the query vector toward a "wrong" cluster, moving it further away from the true target.

### 2. Over-fitting
If $\beta$ is too high and the set of relevant documents is very small, the query might become too specific to those few documents, failing to retrieve other relevant documents that are slightly different.

See also: [[concepts/Vector-Space-Model]], [[concepts/Cosine-Similarity]], [[concepts/Information-Retrieval]]
