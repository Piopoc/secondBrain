# Tokenization

**Tokenization** is the first step of the lexical analysis pipeline in IR. It is the process of breaking a raw stream of text into individual units called **tokens** (usually words).

## Process
1. **Splitting**: Text is typically split based on whitespace and punctuation.
2. **Normalization**: Tokens are often converted to lowercase to ensure case-insensitive matching.

## Challenges and Pitfalls
- **Entity Destruction**: Simple tokenizers may split critical entities like URLs, email addresses, or chemical formulas.
- **Language Specifics**: Languages without clear word boundaries (e.g., Chinese, Japanese) require specialized tokenizers based on dictionaries or statistical models.

See also: [[Lucene-Analyzer]], [[N-Grams]]
