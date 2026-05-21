# Meaningfulness

In the context of measurement theory, **meaningfulness** refers to whether a statistical operation or a statement about data is appropriate given the measurement scale of that data.

## Definition
A statement about a statistical operation is **empirically meaningful** if its truth or falsity is **invariant under permissible transformations** of the underlying scale.

## Meaningfulness vs. Truth
It is critical to distinguish between these two concepts:
- **Truth:** Whether a statement is factually correct.
- **Meaningfulness:** Whether the operation used to reach that statement is valid for the scale.

A statement can be:
1. **Meaningful and True.**
2. **Meaningful and False.**
3. **Meaningless but True** (by coincidence in one specific scale, but the truth changes if the scale is transformed).
4. **Meaningless and False.**

## Example: Temperature (Interval Scale)
Temperature in Celsius is an interval scale. Permissible transformations are affine ($F = C \times \frac{9}{5} + 32$).

- **Meaningful Statement:** "The mean temperature in Paris is less than in Rome."
  - The mean is invariant under affine transformations. If it's true in Celsius, it's true in Fahrenheit.
- **Meaningless Statement:** "The geometric mean of temperature in Paris is greater than in Rome."
  - The geometric mean involves multiplication/division, which is not permitted on interval scales. The truth of this statement can change when converting from Celsius to Fahrenheit.

## Importance in IR
If an IR measure (like Reciprocal Rank) is only on an ordinal scale, computing its arithmetic mean may be technically "meaningless" because the mean is not invariant under monotonic transformations. This is a central point of debate in IR evaluation.
