---
date: 2026-05-16
source: [[raw/12/]]
tags: [neural-networks, logistic-regression, language-modeling, machine-learning]
---

# Summary: Neural Networks and Logistic Regression (raw/12)

This source provides a theoretical and mathematical foundation for neural networks, starting from simple linear classifiers to feedforward architectures for language modeling.

## 1. Logistic Regression
- **Binary Logistic Regression**: Predicts probability using the [[Sigmoid Function]]. Optimized with [[Cross-entropy Loss]] and [[Stochastic Gradient Descent]].
- **Multinomial Logistic Regression**: Generalization to $K$ classes using the [[Softmax Function]].

## 2. Feedforward Neural Networks (FFNN)
- **Architecture**: Acyclic multi-layer networks.
- **Neural Unit**: Performs weighted sums followed by an [[Activation Function]].
- **Neural Language Models**: Uses a fixed context window of words, represented via [[One-hot Encoding]] and transformed into [[Embedding Vector]]s to predict the next word.
- **Training**: Employs [[Self-Supervision]] and [[Cross-entropy Loss]] optimized via [[Stochastic Gradient Descent]].

## 3. Recurrent Neural Networks (RNN)
- **Concept**: Designed for sequential data by introducing a [[Hidden State]] that acts as memory, carrying context from previous time steps.
- **Mechanism**: $h_t = g(U h_{t-1} + W x_t)$ and $y_t = \text{softmax}(V h_t)$.
- **Limitations**: Suffers from the [[Vanishing Gradient Problem]] and cannot be parallelized.
- **LSTM**: A variant that solves context management by selectively adding/removing information.
- **Language Modeling**: Uses [[Teacher Forcing]] during training to predict the next token.
- **Generation**: Implements [[Autoregressive Generation]] to incrementally produce text.

## 4. Encoder-Decoder & Attention
- **Encoder-Decoder**: An architecture where an encoder compresses input into a [[Context Vector]], which a decoder then expands into output.
- **Attention Mechanism**: Solves the "bottleneck" of the fixed context vector by allowing the decoder to access all encoder hidden states via a weighted sum (e.g., [[Dot-product Attention]]).

## 5. Transformers
- **Innovation**: Replaces recurrence with [[Self-Attention]], enabling massive parallelization and better long-range dependency handling.
- **Internal Mechanics**:
    - **[[Query Key Value]]**: The fundamental mechanism for calculating attention weights.
    - **[[Multi-Head Attention]]**: Allows attending to different representation subspaces simultaneously.
    - **Transformer Block**: Combines attention with [[Residual Connection]]s and [[Layer Normalization]] for stability.
- **Architectures**:
    - **Decoder-only**: Causal models used for autoregressive generation.
    - **[[Encoder-only Transformer]]**: Bidirectional models used for understanding and representation.
    - **[[Encoder-Decoder Transformer]]**: Used for seq2seq tasks (e.g., Translation). Features a [[Cross-Attention]] layer where the decoder queries the encoder's output.
- **Input Processing**: Uses [[Subword Tokenization]] and [[Positional Embedding]]s to handle text and order. Employs [[Weight Tying]] between embeddings and output layers.
- **Training**: Follows a two-stage process: [[Pre-Training]] (self-supervised on large data) followed by [[Fine-Tuning]] for specific tasks.

## 6. BERT-style Training & Representation
- **[[Masked Language Modeling]] (MLM)**: A "fill-in-the-blank" ([[Cloze Task]]) objective for bidirectional encoders.
- **[[Next Sentence Prediction]] (NSP)**: Training objective to understand relationships between sentence pairs.
- **Special Tokens**: Uses `[[CLS Token]]` for sequence representation and `[[SEP Token]]` for boundaries.
- **Embeddings**: Uses [[Segment Embedding]] to distinguish between input sentences.
- **[[Contextual Embedding]]**: Representations where the meaning of a token depends on its surrounding context.

## 7. LLM Generation & Decoding
- **Conditional Generation**: Generating text based on a prompt.
- **[[Decoding Strategies]]**: Methods to select the next token.
    - Deterministic: [[Greedy Decoding]].
    - Stochastic: Top-k, Top-p, and Temperature sampling.
    - Heuristic Search: [[Beam Search]] for finding high-probability sequences.
- **T5 Model**: A unified "text-to-text" framework using an encoder-decoder architecture.
