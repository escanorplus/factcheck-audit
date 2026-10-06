# Learning resources

Mapped to `LEARNING_CHECKLIST.md`. Resources are listed by name with the site to find them on.
Titles and availability change, so if a link moves, search the exact title.
Free unless noted. Prefer one main resource per topic and finish it before adding another.

## Phase 1: Foundations

### Python
- **Automate the Boring Stuff with Python** (Al Sweigart), free online at automatetheboringstuff.com. Chapters 1-9 and 16 first.
- **Python for Everybody** (Dr. Chuck), free on freeCodeCamp's YouTube channel and at py4e.com. Good if you prefer video.
- **Kaggle Learn: Python**, free at kaggle.com/learn. Short exercises with instant checking.
- **Practice:** exercism.org (Python track, free, with mentor feedback), and Advent of Code for later.

### Git and GitHub
- **Pro Git** (Scott Chacon), free at git-scm.com/book. Chapters 1-3.
- **freeCodeCamp: Git and GitHub for Beginners** on YouTube.
- **Learn Git Branching**, interactive game at learngitbranching.js.org.

### Jupyter and VS Code
- Search the VS Code docs for "Jupyter Notebooks in VS Code".

### pandas, NumPy, plotting
- **Kaggle Learn: Pandas** and **Data Visualization**, free.
- **pandas "10 minutes to pandas"**, in the official docs at pandas.pydata.org.
- **Python Data Science Handbook** (Jake VanderPlas), free online at jakevdp.github.io/PythonDataScienceHandbook. Chapters on NumPy, pandas, matplotlib.
- **Corey Schafer's pandas tutorials** on YouTube.

### ML basics and statistics
- **Machine Learning Specialization** (Andrew Ng), Coursera, free to audit. Course 1 and 2.
- **Kaggle Learn: Intro to Machine Learning** and **Intermediate Machine Learning**.
- **StatQuest with Josh Starmer** on YouTube. Search each topic: "StatQuest confidence intervals", "StatQuest ROC and AUC", "StatQuest cross validation", "StatQuest logistic regression", "StatQuest bootstrapping".
- **scikit-learn user guide**, at scikit-learn.org. Read the sections on model evaluation and cross-validation.
- **Think Stats** (Allen Downey), free at greenteapress.com. Statistics through code.
- **Khan Academy: Statistics and Probability**, if the basics feel shaky.

## Phase 2: NLP and transformers
- **Hugging Face LLM / NLP Course**, free at huggingface.co/learn. The best single resource for this phase.
- **The Illustrated Transformer** (Jay Alammar), jalammar.github.io.
- **Speech and Language Processing** (Jurafsky and Martin), free draft at web.stanford.edu/~jurafsky/slp3. Use as reference for TF-IDF and embeddings.
- **Stanford CS224N** (NLP with Deep Learning), lectures free on YouTube. Optional, for depth.
- **Andrej Karpathy: Neural Networks, Zero to Hero**, YouTube. Optional intuition for how models learn.

## Phase 3: Domain knowledge

### Retrieval and RAG
- **Hugging Face course**, sections on semantic search and FAISS.
- **Sentence-Transformers documentation**, at sbert.net.
- **FAISS** wiki on GitHub (facebookresearch/faiss), and the **Chroma** docs.
- **BM25:** search "BM25 explained" and the `rank_bm25` Python package.
- The original **RAG paper** (Lewis et al. 2020), on arXiv.

### Fact-checking
- Papers listed in `reports/Fact checking audit paper survey.md`, in its suggested reading order.
- For each paper, first read the abstract, introduction, results and limitations. Write one paragraph of notes.

### Calibration, fairness, robustness
- **On Calibration of Modern Neural Networks** (Guo et al. 2017), on arXiv.
- **scikit-learn:** the "Probability calibration" page of the user guide.
- **Fairness and Machine Learning** (Barocas, Hardt, Narayanan), free at fairmlbook.org. Start with the introduction and the classification chapter.
- **Fairlearn documentation**, at fairlearn.org. The `MetricFrame` user guide.
- **CheckList** paper (Ribeiro et al. 2020), on arXiv, for behavioural testing.

## Phase 4+: Engineering and writing
- **FastAPI tutorial**, official, at fastapi.tiangolo.com.
- **Docker Get Started**, official, at docs.docker.com.
- **pytest documentation**, at docs.pytest.org.
- **MLflow tutorials**, at mlflow.org.
- **Made With ML** (Goku Mohandas), free at madewithml.com, for the MLOps big picture.
- **How to read a paper** (S. Keshav), a short three-pass method; search the title.

## Weekly rhythm that works
- Study session: 1-2 hours of learning, then 1 hour of coding it yourself.
- End of week: tick the checklist, write 5 lines on what you learned, commit.
- Ask me when stuck. I can explain a concept, set exercises, or review your code.
