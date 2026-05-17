# Transformer

The **Transformer** is a deep learning architecture based on an encoder-decoder structure and the **Self-Attention** mechanism.

## Main Innovation: Self-Attention
Unlike RNNs, Transformers do not process data sequentially. Self-attention allows the model to:
- **Parallelize** computation significantly.
- Learn **long-range dependencies** more effectively by attending to all tokens in a sequence simultaneously.

## Variants
- **Encoder-only**: Best for understanding full sequences (e.g., [[BERT]]).
- **Decoder-only**: Best for text generation (e.g., [[GPT]]).
- **Causal Transformers**: Consider only previous tokens in the sequence (left-to-right).

See also: [[BERT]], [[Word Embedding]]
