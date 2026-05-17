# Cosine Similarity

**Cosine Similarity** is a metric used to measure how similar two vectors are, regardless of their magnitude.

## Mathematical Definition
It is defined as the cosine of the angle $\theta$ between two vectors $\vec{A}$ and $\vec{B}$:
$$\text{similarity} = \cos(\theta) = \frac{\vec{A} \cdot \vec{B}}{\|\vec{A}\| \cdot \|\vec{B}\|}$$

## Properties
- **Range**: The value ranges from $-1$ to $1$ (though in IR, since term frequencies are non-negative, it ranges from $0$ to $1$).
- **Interpretation**: $1$ means the vectors are identical in direction; $0$ means they are orthogonal (no common terms).

## Use in IR
It is the standard measure for the [[Vector-Space-Model]] and is also used to compare [[Word-Embedding]] vectors.

See also: [[Vector-Space-Model]], [[Word-Embedding]]
