# Representational Measurement Theory

The **Representational Theory of Measurement** provides the formal mathematical foundation for understanding how empirical observations are mapped to numerical values.

## Core Principles

The theory is based on three main pillars:

1. **Empirical Relations:** The existence of a way to compare entities based on an attribute (e.g., "Object A is longer than Object B").
2. **Concatenation:** The ability to combine entities to create a new entity with a combined attribute (e.g., placing two rods end-to-end).
3. **Homomorphism ($\phi$):** A measurement scale is a function $\phi$ that maps entities into numbers such that the empirical relation is preserved as a numerical relation:
   - $e_1 \preceq e_2 \iff \phi(e_1) \le \phi(e_2)$
   - $\phi(e_1 \circ e_2) = \phi(e_1) + \phi(e_2)$

## Difference Structures and Interval Scales

To establish an **Interval Scale**, the theory uses a **difference structure**. A difference structure is a set of objects with a binary relation $\preceq_d$ on pairs of objects (intervals) that satisfies four axioms:
1. **Weak Order:** Intervals can be ordered.
2. **Sign Symmetry:** If $\Delta_{ab} \preceq_d \Delta_{cd}$, then $\Delta_{dc} \preceq_d \Delta_{ba}$.
3. **Weak Monotonicity:** $\Delta_{ab} \preceq_d \Delta_{a'b'}$ and $\Delta_{bc} \preceq_d \Delta_{b'c'} \implies \Delta_{ac} \preceq_d \Delta_{a'c'}$.
4. **Solvability:** Ensures the existence of intermediate elements.

### Representation Theorem
If a set of objects forms a difference structure, there exists a measure function $m: A \to \mathbb{R}$ such that:
$$\Delta_{ab} \preceq_d \Delta_{cd} \iff m(a) - m(b) \ge m(c) - m(d)$$

### Uniqueness Theorem
The resulting interval scale is unique up to an affine transformation: $m^*(a) = \alpha m(a) + \beta$ (where $\alpha > 0$).

## Application to IR
In IR, the challenge is that there is often no natural "empirical ordering" for retrieval effectiveness. Therefore, IR measures are often "artificial" constructions. The goal of a general theory of IR measures is to construct these orders and intervals formally to derive interval-scale measures.
