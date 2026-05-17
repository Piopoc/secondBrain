# Boolean Model

The **Boolean Model** is the simplest retrieval model, based on set theory and Boolean algebra.

## Logic
A query is an expression of terms combined with operators: **AND**, **OR**, and **NOT**. A document is either relevant (1) or not relevant (0) based on whether it satisfies the Boolean expression.

## Characteristics
- **No Ranking**: Results are returned as an unordered set.
- **Exact Match**: It requires the user to specify exactly which terms must be present.
- **Efficiency**: Extremely fast processing using inverted indices.

## Limitations
- **Binary Nature**: Does not consider term frequency or partial matches.
- **User Burden**: The user must construct the perfect query to get useful results.

See also: [[Vector-Space-Model]], [[Information-Retrieval]]
