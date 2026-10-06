# Learning checklist

Tick items by changing `[ ]` to `[x]`. An item is done when you can explain it in your own words
and have used it in code, not when you have only watched a video.

## Phase 1: Foundations (weeks 1-6)

### Python
- [ ] Functions, loops, conditionals
- [ ] Lists, dicts, sets, comprehensions
- [ ] Reading and writing files, JSON, CSV
- [ ] Classes (basic)
- [ ] Virtual environments and `pip`
- [ ] Reading error messages and debugging
- [ ] Exercise 1: `exercises/ex1.py` (`word_counts`)

### Tools
- [ ] Git: commit, branch, push, `.gitignore`
- [ ] GitHub repo created and pushed
- [ ] Jupyter notebooks in VS Code

### pandas and NumPy
- [ ] Load, inspect and clean a CSV
- [ ] Filter, group, merge, handle missing values
- [ ] Plot with matplotlib

### ML basics and statistics
- [ ] Train/validation/test split and why
- [ ] Overfitting and cross-validation
- [ ] Logistic regression and gradient boosting (scikit-learn)
- [ ] Accuracy, precision, recall, F1, macro vs micro
- [ ] ROC and PR curves, confusion matrix
- [ ] Confidence intervals and bootstrapping
- [ ] Significance tests and multiple-comparison problem

## Phase 2: NLP and transformers (weeks 7-10)
- [ ] Tokenisation and TF-IDF
- [ ] Word and sentence embeddings
- [ ] LIAR baseline: TF-IDF + logistic regression
- [ ] Attention and transformers, high level
- [ ] Hugging Face `transformers` and `datasets`
- [ ] Fine-tune DistilBERT on Colab, run on laptop

## Phase 3: Domain knowledge (weeks 11-14)
- [ ] Retrieval: BM25, dense search, recall@k
- [ ] Vector search with FAISS or Chroma
- [ ] RAG: retrieve then verify, with citations
- [ ] Claim verification setup (claim, evidence, label)
- [ ] Dataset artifacts: claim-only baselines, leakage
- [ ] Calibration: ECE, reliability diagrams, temperature scaling
- [ ] Subgroup fairness: disaggregated metrics
- [ ] Robustness: paraphrase and typo perturbations
- [ ] Read the survey papers in the suggested order (`reports/Fact checking audit paper survey.md`)
- [ ] Write the related-work notes and one sharp research question

## Phase 4+: Build, audit, ship
- [ ] Evaluation harness
- [ ] RAG verdict pipeline
- [ ] Audit suite (calibration, slices, robustness)
- [ ] Mitigation with before/after numbers
- [ ] FastAPI, Docker, pytest, MLflow
- [ ] CI audit gate
- [ ] README, demo and write-up
