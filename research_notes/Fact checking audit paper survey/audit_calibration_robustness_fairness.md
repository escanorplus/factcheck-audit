# Auditing NLP/LLM systems (fact-checkers): calibration, robustness, fairness, drift

Verification note: every paper below was returned by search and/or fetched this session (arXiv/ACL Anthology/publisher pages). Items marked [search-only] were confirmed via search snippets with title/authors/ID but not fetched in full. The ScienceDirect paper (cross-language unfairness) returned 403 on fetch; details come from the search snippet only. Library facts (netcal, MAPIE, fairlearn) come from search snippets of docs/PyPI/GitHub. Some items I know from background (e.g. Platt scaling, ACE/SCE details) are only cited where a source was seen.

## Q1. Which calibration, robustness and fairness metrics are standard and which are criticised?

### Takeaway
ECE (binned) with reliability diagrams and temperature scaling is the de facto calibration standard (Guo et al. 2017), but ECE is criticised as binning-sensitive and non-proper; audit layers should report proper scores (Brier/NLL), adaptive/class-conditional variants, and conformal coverage. Robustness is standardly reported as accuracy drop / invariance failure rate under perturbations (CheckList, TextAttack, TextFlint, PromptBench). Fairness is standardly reported as disaggregated (per-subgroup) metrics and gaps (fairlearn MetricFrame), with formal criteria (independence/separation/sufficiency) from Barocas-Hardt-Narayanan.

### Cited Findings

#### Calibration (foundational)
- Guo, Pleiss, Sun, Weinberger. "On Calibration of Modern Neural Networks." ICML 2017. Modern nets are poorly calibrated; depth, width, weight decay, batch norm affect it; temperature scaling (single-parameter Platt variant) is surprisingly effective. — [arXiv:1706.04599](https://arxiv.org/abs/1706.04599)
- Desai & Durrett. "Calibration of Pre-trained Transformers." EMNLP 2020, pp. 295-302. BERT/RoBERTa on SNLI/MNLI, QQP/TPPDB, SWAG/HellaSWAG: calibrated in-domain out of the box; out-of-domain calibration error up to 3.5x lower than baselines (post-hoc temperature scaling helps further). Code: github.com/shreydesai/calibration. — [ACL Anthology](https://aclanthology.org/2020.emnlp-main.21/)
- Minderer et al. "Revisiting the Calibration of Modern Neural Networks." NeurIPS 2021. Recent non-convolutional (ViT-type) models are among the best calibrated; accuracy and calibration are not simply anti-correlated (image domain, so transfer to NLP is an inference). — [NeurIPS PDF](https://proceedings.neurips.cc/paper/2021/file/8420d359404024567b5aefda1231af24-Paper.pdf)

#### ECE and its flaws
- Nixon et al. "Measuring Calibration in Deep Learning." CVPR Workshops 2019. Criticises ECE: bin-count choice is arbitrary and can substantially change the value; proposes Static Calibration Error (SCE), Adaptive Calibration Error (ACE), Thresholded ACE; finds class-conditional evaluation and L2 norm work better. — [CVPRW PDF](https://openaccess.thecvf.com/content_CVPRW_2019/papers/Uncertainty%20and%20Robustness%20in%20Deep%20Visual%20Learning/Nixon_Measuring_Calibration_in_Deep_Learning_CVPRW_2019_paper.pdf)
- ECE is not a proper scoring rule; a constant-marginal predictor with no discriminative power can achieve ECE = 0. — [Better Uncertainty Calibration via Proper Scores, arXiv:2203.07835](https://arxiv.org/pdf/2203.07835) (found via search; the zero-ECE claim was stated in search-result summaries of ECE critiques, e.g. [Emergent Mind overview](https://www.emergentmind.com/topics/expected-calibration-error); treat the latter as secondary).
- Survey: "Calibration in Deep Learning: A Survey of the State-of-the-Art" (arXiv 2023). [search-only] — [arXiv:2308.01222](https://arxiv.org/pdf/2308.01222)
- "Beyond ECE: Calibrated Size Ratio, Risk Assessment, and Confidence-Weighted Metrics" (arXiv 2605.01796) is a recent critique; [search-only, not read] — [arXiv](https://arxiv.org/html/2605.01796)

#### LLM calibration and verbalised confidence
- Kadavath et al. (Anthropic). "Language Models (Mostly) Know What They Know." 2022. Larger models are well-calibrated on multiple-choice/true-false in the right format; P(True) self-evaluation separates correct from incorrect; calibration degrades out-of-distribution. — [arXiv:2207.05221](https://arxiv.org/pdf/2207.05221)
- Tian, Mitchell, Zhou, Sharma, Rafailov, Yao, Finn, Manning. "Just Ask for Calibration: Strategies for Eliciting Calibrated Confidence Scores from Language Models Fine-Tuned with Human Feedback." EMNLP 2023. Verbalised confidence from RLHF models (ChatGPT, GPT-4, Claude) is typically better calibrated than raw token probabilities; prompting for several candidate answers first helps; reported ECE reduction >50% on some QA datasets. — arXiv:2305.14975 (ID from search result; [snippet source](https://x.com/fly51fly/status/1733845055067357589) is secondary — verify at https://arxiv.org/abs/2305.14975 before final citation)
- Recent (2025-26) verbalised-confidence work surfaced by search, not read: "Same Answer, Different Confidence: Protocol Sensitivity in LLM Confidence Calibration" ([arXiv:2605.27752](https://arxiv.org/pdf/2605.27752)); "Calibration as a First-Class Criterion in LLM Evaluation" ([arXiv:2609.26489](https://arxiv.org/html/2609.26489v1)); "Calibrating Verbalized Confidence with Self-Generated Distractors" ([arXiv:2509.25532](https://arxiv.org/pdf/2509.25532)); "Large Language Model Confidence Estimation via Black-Box Access" ([arXiv:2406.04370](https://arxiv.org/pdf/2406.04370)). [search-only]

#### Conformal prediction for NLP/LLMs
- Campos, Farinhas, Zerva, Figueiredo, Martins. "Conformal Prediction for Natural Language Processing: A Survey." TACL 2024. Model-agnostic, distribution-free coverage guarantees; covers applications and open challenges. — [arXiv:2405.01976](https://arxiv.org/abs/2405.01976), [TACL PDF](https://aclanthology.org/2024.tacl-1.82.pdf)
- Quach et al. "Conformal Language Modeling." ICLR 2024. Calibrates a stopping rule for sampling so the returned set contains at least one acceptable answer with high probability. — [arXiv:2306.10193](https://arxiv.org/pdf/2306.10193)
- Su et al. (title seen) "API Is Enough: Conformal Prediction for Large Language Models Without Logit-Access" (arXiv 2403.01216) — relevant to black-box fact-checker APIs. [search-only; author list not verified] — [arXiv](https://arxiv.org/html/2403.01216v1)
- "Conformal Alignment: Knowing When to Trust Foundation Models with Guarantees" (arXiv 2405.10301); "Domain-Shift-Aware Conformal Prediction for LLMs" (arXiv 2510.05566). [search-only] — [1](https://arxiv.org/pdf/2405.10301), [2](https://arxiv.org/html/2510.05566v1)

#### Behavioural testing / robustness
- Ribeiro, Wu, Guestrin, Singh. "Beyond Accuracy: Behavioral Testing of NLP Models with CheckList." ACL 2020 (Best Paper). Capability-based tests: Minimum Functionality (MFT), Invariance (INV), Directional Expectation (DIR); practitioners with CheckList found ~3x more bugs. Code: github.com/marcotcr/checklist. — [ACL Anthology](https://aclanthology.org/2020.acl-main.442/)
- Morris et al. "TextAttack: A Framework for Adversarial Attacks, Data Augmentation, and Adversarial Training in NLP." EMNLP 2020 demos. Attacks = goal function + constraints + transformation + search; 16 attacks; pip package `textattack`. — [arXiv:2005.05909](https://arxiv.org/abs/2005.05909), [GitHub](https://github.com/QData/TextAttack)
- Gui et al. "TextFlint: Unified Multilingual Robustness Evaluation Toolkit for NLP." ACL 2021 demos. 20 general + 60 task-specific transformations, subpopulation, adversarial attacks. — [ACL Anthology](https://aclanthology.org/2021.acl-demo.41/), [arXiv:2103.11441](https://arxiv.org/pdf/2103.11441)
- Wu et al. "Polyjuice: Generating Counterfactuals for Explaining, Evaluating, and Improving Models." ACL 2021. Controllable counterfactual generator (fine-tuned GPT-2). — [ACL Anthology](https://aclanthology.org/2021.acl-long.523/)
- Zhu et al. "PromptBench / PromptRobust: Towards Evaluating the Robustness of LLMs on Adversarial Prompts." Char/word/sentence/semantic prompt attacks; 4,788 adversarial prompts, 13 datasets; word-level attacks most damaging (39% avg drop). Library paper: arXiv:2312.07910. — [arXiv:2306.04528](https://arxiv.org/pdf/2306.04528), [library](https://arxiv.org/pdf/2312.07910)
- Thorne & Vlachos et al. "The FEVER2.0 Shared Task." FEVER workshop 2019 (build/break/fix; breakers submitted 1,174 claims). — [ACL Anthology D19-6601](https://aclanthology.org/D19-6601/)
- Thorne, Vlachos, et al. "Adversarial attacks against Fact Extraction and VERification" (arXiv 2019; FEVER2.0 baseline attacks). — [arXiv:1903.05543](https://arxiv.org/pdf/1903.05543)
- Liu, Abuadbba, Moore, Nepal, Paris, Wu, Yang, Sheng. "Adversarial Attacks Against Automated Fact-Checking: A Survey." EMNLP 2025 Main. Categorises attacks on claims, evidence, claim-evidence pairs, and defences. — [arXiv:2509.08463](https://arxiv.org/abs/2509.08463)
- Schuster, Shah, Yeo, Filizzola, Santus, Barzilay. "Towards Debiasing Fact Verification Models." EMNLP 2019. Claim-only BERT gets 61.7% on FEVER (majority 33.3%); negation cues correlate with REFUTES; builds a symmetric eval set where FEVER-trained models drop significantly. — [arXiv:1908.05267](https://arxiv.org/abs/1908.05267)

#### Fairness
- Barocas, Hardt, Narayanan. "Fairness and Machine Learning: Limitations and Opportunities." MIT Press 2023; free at [fairmlbook.org](https://fairmlbook.org/). Covers formal non-discrimination criteria in a decision-theoretic setting, their limits, and legal context.
- Bird et al. "Fairlearn" (toolkit paper): "Fairlearn: Assessing and Improving Fairness of AI Systems," arXiv 2303.16626 (Weerts et al.; author list from memory, not verified). `fairlearn.metrics.MetricFrame` does disaggregated evaluation over one or more sensitive features. — [arXiv:2303.16626](https://arxiv.org/pdf/2303.16626), [MetricFrame docs](https://fairlearn.org/v0.14/api_reference/generated/fairlearn.metrics.MetricFrame.html)

### Inferences
- Report ECE only alongside Brier/NLL and a reliability diagram, using adaptive binning (ACE) or equal-mass bins and class-conditional ECE (given the Nixon critique and non-proper-score issue); for fact-check verdicts (3-class SUPPORTS/REFUTES/NEI), top-label ECE hides class-wise miscalibration.
- Conformal prediction gives a fact-checker an auditable guarantee ("verdict set contains truth >= 1-alpha") that does not depend on ECE; marginal coverage should be checked per subgroup (topic/region) since guarantees are only marginal. (Marginal-only nature is standard CP theory; not separately sourced here.)
- For black-box LLM fact-checkers, verbalised confidence + sampling consistency are the practical options; Tian et al. support verbalised > raw logits for RLHF models, but 2025-26 protocol-sensitivity work (unread) suggests results are prompt-dependent.

### Gaps
- I did not locate a single authoritative paper on "ECE flaws" specific to LLMs; criticisms come from vision/ML literature (Nixon, proper-score papers). Gupta et al. / Widmann et al. / Kumar et al. (debiased ECE, "Verified Uncertainty Calibration") are known to exist but I did not verify them this session.
- Conformal prediction applied specifically to claim verification: not found in this search.
- FEVER2.0 baseline paper author list/venue for arXiv:1903.05543 not verified beyond search snippet.

## Q2. How can fairness be defined for claim verification where there are no obvious protected attributes?

### Takeaway
Existing work treats topic, political connotation/leaning, language/region (nationality, religion), time and publisher/source as the "groups", and measures (a) disaggregated performance gaps, (b) minimal-pair consistency (counterfactual invariance), (c) source-preference bias. No consensus framework exists; this is open.

### Cited Findings
- PolBiX (Jakob, Harbecke, Parschan, Neves, Schmitt; Findings of EMNLP 2025): minimal pairs of factually equivalent German claims differing only in political connotation (euphemism/dysphemism); judgmental words significantly change truthfulness assessment across six LLMs, persisting even when prompted to be objective. This is a counterfactual-invariance fairness definition. — [arXiv:2509.15335](https://arxiv.org/abs/2509.15335)
- "Performance unfairness of large language models in cross-language fact-checking," Information Processing & Management (ScienceDirect, 2026). Per search snippet: for English and Portuguese claims political bias accounted for the largest share of performance unfairness; for other languages nationality, then religious or political bias. Authors/abstract not retrieved (403). — [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0306457326000087) [search snippet only]
- Proma, Pate, Druckman, Ghoshal, He, Hoque. "How LLMs Fail to Support Fact-Checking." (arXiv Feb 2025, rev. Sep 2025). ChatGPT/Gemini/Claude struggle to ground responses in real news sources and tend to cite left-leaning sources. — [arXiv:2503.01902](https://arxiv.org/abs/2503.01902)
- Bakke & Heggelund. "(Fact) Check Your Bias." arXiv June 2025. HerO (FEVER-25 baseline) with Llama 3.1: ~half of claims labelled "Not Enough Evidence" when relying on parametric knowledge; ~50% of retrieved evidence unique to each injected perspective; final verdicts nevertheless stayed relatively stable. — [arXiv:2506.21745](https://arxiv.org/abs/2506.21745)
- "Political Bias Audits of LLMs Capture Sycophancy to the Inferred Auditor" (arXiv 2604.27633): audit outcomes depend on who the model thinks is asking; single-questionnaire audits unreliable. Authors not retrieved. — [arXiv](https://arxiv.org/pdf/2604.27633) [search-only]
- Verhoeven, Mishra, Shutova. "Yesterday's News: Benchmarking Multi-Dimensional OOD Generalization of Misinformation Detection Models." Computational Linguistics (accepted Nov 2025). misinfo-general: generalisation across time, event, topic, publisher, political bias, misinformation type, with attention to shortcuts. This is effectively a subgroup/slice framework for misinformation. — [arXiv:2410.18122](https://arxiv.org/abs/2410.18122), [DOI](https://doi.org/10.1162/COLI.a.585)
- Dataset bias: topic imbalance between true and false items (e.g. police topics more frequent in false news in Snopes data; technology/environment in Emergent), selection bias from fact-checker-sourced data, and diachronic bias. — [Fake News Detection: It's All in the Data! (arXiv:2407.02122)](https://arxiv.org/html/2407.02122v2) (the specific Snopes/Emergent examples come from search snippets of this and related surveys; verify before quoting); [Mitigation of Diachronic Bias in Fake News Detection Dataset, arXiv:2108.12601](https://arxiv.org/pdf/2108.12601)
- Formal criteria (independence, separation, sufficiency) apply once a "group" variable is defined; the book treats the choice of groups and the limits of statistical criteria. — [fairmlbook.org](https://fairmlbook.org/)

### Inferences
- A workable operational definition: define pseudo-protected attributes as metadata slices (topic cluster, claimed-actor political leaning, geography/language, source/publisher, claim age) and require (1) bounded gaps in accuracy/macro-F1 and in calibration (ECE per slice) via MetricFrame; (2) invariance of verdict under connotation-swapping or entity-swapping minimal pairs (PolBiX/CheckList INV); (3) separation-style parity (equal FPR/FNR of "false" labels across slices), noting that base rates of falsehood legitimately differ by topic, so independence/demographic parity is inappropriate and separation or calibration-within-groups is the better fit.
- Fairness of evidence retrieval/source selection (left-leaning citation preference) is a distinct, retrieval-stage axis needed in fact-checking pipelines.
- Slice labels will be noisy/inferred (LLM-assigned leaning), so uncertainty in group assignment should be reported (fairlearn handles only supplied attributes).

### Gaps
- No source found that formally defines fairness for claim verification with non-protected attributes; the above is my synthesis.
- Fairlearn's treatment of intersectional/many-slice small-sample CIs: not verified in docs this session.
- Evidence for causal (not just correlational) topic/leaning effects is thin; PolBiX is the strongest, German-only.

## Q3. What existing work audits fact-checkers specifically, and what is missing?

### Takeaway
Existing audits are mostly one-axis: adversarial robustness (FEVER2.0, survey), claim-only/dataset artefacts (Schuster), dynamic LLM evaluation (FACT-AUDIT), political-bias probes (PolBiX, Proma et al.), cross-language unfairness, and OOD/temporal generalisation. No integrated, automated, continuous audit layer covering calibration + robustness + fairness + drift for a deployed fact-checker was found.

### Cited Findings
- Lin, Deng, Gu, Zhang, Ma, Ng, Chua. "FACT-AUDIT: An Adaptive Multi-Agent Framework for Dynamic Fact-Checking Evaluation of LLMs." arXiv Feb 2025. Multi-agent + importance sampling to generate adaptive datasets; evaluates verdict prediction and justification. — [arXiv:2502.17924](https://arxiv.org/abs/2502.17924)
- FEVER2.0 build-break-fix and adversarial survey (above). — [D19-6601](https://aclanthology.org/D19-6601/), [arXiv:2509.08463](https://arxiv.org/abs/2509.08463)
- Counterfactual Debiasing for Fact Verification (ACL 2023 long paper) — mitigation of claim-only bias. Authors not retrieved. — [ACL Anthology PDF](https://aclanthology.org/2023.acl-long.374.pdf) [search-only]
- Temporal: Lazaridou et al. "Mind the Gap: Assessing Temporal Generalization in Neural Language Models." NeurIPS 2021 — stale models degrade as test period moves away from training (up to 16% perplexity difference vs a model trained on test-period data, per the search summary). — [arXiv:2102.01951](https://arxiv.org/abs/2102.01951)
- Temporal concept drift and explanations: "On the Impact of Temporal Concept Drift on Model Explanations" (Findings of EMNLP 2022). Authors not retrieved. — [ACL Anthology](https://aclanthology.org/2022.findings-emnlp.298.pdf) [search-only]
- Time-aware fact-checking: "Evidence-Based Temporal Fact Verification" ([arXiv:2407.15291](https://arxiv.org/html/2407.15291v2)); "Implicit Temporal Reasoning for Evidence-Based Fact-Checking" (Findings of EACL 2023, [arXiv:2302.12569](https://arxiv.org/abs/2302.12569)); "TSVer" (EMNLP 2025, [ACL Anthology](https://aclanthology.org/2025.emnlp-main.1519.pdf)); time-aware models reported up to 9% Micro-F1 gain over base models (search summary, unverified). [search-only]
- Drift for fake news: "Learn over Past, Evolve for Future: Forecasting Temporal Trends for Fake News Detection" ([arXiv:2306.14728](https://arxiv.org/html/2306.14728)); "Wild-Time" benchmark of distribution shift over time ([arXiv:2211.14238](https://arxiv.org/pdf/2211.14238)). [search-only]

### Practical tooling (Python)
- netcal (EFS-OpenSource calibration-framework; `pip install netcal`): metrics (ECE, ACE, MCE and others), scaling/binning calibrators incl. temperature scaling, histogram binning — [GitHub](https://github.com/EFS-OpenSource/calibration-framework), [API docs](https://efs-opensource.github.io/calibration-framework), [PyPI](https://pypi.org/project/netcal/)
- MAPIE (scikit-learn-contrib): conformal prediction intervals/sets for regression and multi-class classification; docs mention newer risk-control features — [GitHub](https://github.com/scikit-learn-contrib/MAPIE), [docs](https://mapie.readthedocs.io/), [paper arXiv:2207.12274](https://arxiv.org/abs/2207.12274)
- fairlearn: `MetricFrame` for disaggregated metrics — [docs](https://fairlearn.org/v0.14/api_reference/generated/fairlearn.metrics.MetricFrame.html)
- TextAttack, TextFlint, CheckList, PromptBench (links above). scikit-learn provides `brier_score_loss`, `log_loss`, `calibration_curve` (from background knowledge; not source-checked).

### Inferences
- Missing: (1) joint audit layer reporting per-slice calibration + conformal coverage + perturbation invariance; (2) drift monitoring tied to claim time/event (time-aware fact-checking papers study modelling, not audit monitoring); (3) audits of the full pipeline (retrieval + verdict + justification) for fairness, with only partial coverage in "(Fact) Check Your Bias" and Proma et al.; (4) LLM-fact-checker confidence calibration studies on claim verification specifically; (5) standard definitions/thresholds for group fairness over non-protected slices.
- Per-slice conformal coverage and calibration for claim verification appear unstudied (no hit in searches).

### Gaps
- Searches were limited (about 20 calls); I did not exhaustively check ClaimBuster/CheckThat!/AVeriTeC/ClimateFEVER audit-style papers, Mind the Gap's follow-ups on factual-knowledge staleness (e.g. TemporalWiki, "Time Waits for No One"), or FAccT proceedings. Absence of a hit is not proof of absence.
- Several 2026 arXiv IDs (26xx) were found through search only; verify before citing.
