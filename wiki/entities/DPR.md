# DPR (Dense Passage Retriever)

**DPR** is a specific implementation of a **Bi-encoder** used for open-domain question answering.

## Architecture
- Uses a BERT-based encoder for both the query and the document.
- The query and document are mapped to dense vectors.

## Training
DPR is fine-tuned using a contrastive loss with **positive examples** (passages that answer the query) and **negative examples** (randomly sampled irrelevant passages).

See also: [[Bi-encoder]], [[BERT]]
