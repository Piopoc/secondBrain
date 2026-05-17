# TF-IDF (Term Frequency-Inverse Document Frequency)

**TF-IDF** is a numerical statistic used in Information Retrieval to reflect how important a word is to a document in a collection.

### Components
1. **Term Frequency (TF)**: Measures how frequently a term occurs in a document.
   - $\text{TF} \propto \text{Importance of the term in the specific document}$.
2. **Inverse Document Frequency (IDF)**: Measures how common or rare a term is across the entire corpus.
   - $\text{IDF} = \log_2 \frac{N}{n_i}$
   - High IDF means the term is rare and thus has high **resolving power** (it's a good discriminator).

### The Weighting
The final weight is the product: $\text{weight} = \text{TF} \cdot \text{IDF}$.
This ensures that words that appear often in one document but rarely in others are given the highest weight, while common "stopwords" (high TF in all documents) are penalized by a low IDF.

See also: [[summaries/IR/IR - Modelli di Recupero#2. Vector-Space-Model (VSM)]]
