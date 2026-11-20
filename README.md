# Biomedical NLP — Multi-label MeSH Classification

An academic NLP study of **multi-label classification of cardiology publications** from PubMed into **50 MeSH categories**. The workflow covers PubMed/Entrez XML collection, annotation provenance checks, preprocessing and phrase detection, domain-specific Word2Vec training, neural architectures, hyperparameter selection and model comparison.

## Results

| Model | Test micro-F1 | Test macro-F1 |
| --- | ---: | ---: |
| **Word2Vec + BiGRU + Attention (tuned)** | **0.8072** | **0.7753** |
| BiGRU + Attention (untuned) | 0.8049 | 0.7738 |
| TF-IDF + Logistic Regression (tuned) | 0.7873 | 0.7536 |
| TextCNN (tuned) | 0.7861 | 0.7517 |

The notebook documents the data split, validation-based model selection, analysis by MeSH label and error cases. The figures above are results recorded in the original notebook, not a fresh reproduction during publication.

## Methods

- Source: PubMed XML using Biopython Entrez; separate manually indexed publications from automatically indexed records for supervised evaluation.
- Features: Gensim Word2Vec (CBOW and Skip-gram), medical phrase detection and TF-IDF baselines.
- Models: Logistic Regression, MLP, TextCNN and BiGRU + Attention in PyTorch.
- Evaluation: iterative multilabel stratification, validation-tuned decision thresholds, micro/macro-F1 and error analysis.
- Optimization: Optuna, early stopping and checkpoint selection.

## Run

1. Install Python and the dependencies in `requirements.txt` (a compatible GPU environment is recommended for neural models).
2. Set `COURSE_BASE_DIR` to a writable directory. The original notebook otherwise falls back to an author-specific Windows drive path.
3. Set `ENTREZ_EMAIL` to your own email address for NCBI Entrez; `ENTREZ_API_KEY` is optional.
4. Open `biomedical-nlp.ipynb` in Jupyter and run the cells sequentially.

The notebook downloads and processes a large corpus; expect significant storage, runtime and network requirements. **The PubMed corpus and checkpoints are not included in this repository.** The original executed notebook preserves the recorded results.

## Source

- [PubMed](https://pubmed.ncbi.nlm.nih.gov/)
- [NCBI E-utilities](https://www.ncbi.nlm.nih.gov/books/NBK25501/)

## Repository contents

- `biomedical-nlp.ipynb` — full experiment notebook, including preprocessing, EDA, training and results.
- `requirements.txt` — main third-party Python dependencies (version-independent overview).

Academic project; model results are dataset- and split-specific. No clinical claims are made.
