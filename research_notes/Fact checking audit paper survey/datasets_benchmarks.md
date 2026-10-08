# Claim verification / automated fact-checking datasets and benchmarks

Method note: every paper below was confirmed to exist via the ACL Anthology / arXiv page returned by search or fetch. Numbers come from abstracts or fetched pages (summarised by the fetch tool). Where a number could not be confirmed it is listed under Gaps. Full PDFs of AVeriTeC papers could not be parsed, so some table-level numbers (e.g. per-label accuracy) are missing.

## 1. What are the realistic baseline and state-of-the-art numbers on each benchmark?

### Takeaway
Synthetic Wikipedia benchmarks (FEVER) are near-saturated and artifact-prone. Real-world benchmarks remain hard: LIAR six-way accuracy sits around 0.27-0.30 on claim text alone, MultiFC best macro-F1 was 49.2 (2019), and AVeriTeC top score rose from 0.11 (baseline) to 0.63 (2024, GPT-4o, proprietary), but only 0.33 in the 2025 open-weights, single-GPU edition. Gold evidence lifts veracity accuracy by 14-22 points over retrieved evidence, so retrieval is the bottleneck.

### Cited Findings

**FEVER (2018)**
- Thorne, Vlachos, Christodoulopoulos, Mittal. "FEVER: a large-scale dataset for Fact Extraction and VERification." NAACL 2018. [arXiv 1803.05355](https://arxiv.org/abs/1803.05355). 185,445 claims, labels Supported/Refuted/NotEnoughInfo, Fleiss kappa 0.6841, dataset at fever.ai. Baseline figures in the abstract-level fetch: 31.87% (with correct evidence) and 50.91% (label-only); the exact metric attached to each figure was not confirmed — verify in the paper before quoting. Licence: not confirmed in fetched pages (fever.ai hosts it; commonly CC BY-SA for Wikipedia-derived content — unverified).
- Thorne et al. "The Fact Extraction and VERification (FEVER) Shared Task." FEVER workshop @ EMNLP 2018. [ACL W18-5501](https://aclanthology.org/W18-5501/), [arXiv 1811.10971](https://arxiv.org/abs/1811.10971). 23 teams, 19 beat the baseline, best FEVER score 64.21% (UNC-NLP) — [search summary of W18-5501](https://aclanthology.org/W18-5501/); [arXiv abstract page](https://arxiv.org/abs/1811.10971). Pipeline: document selection, sentence selection, NLI.

**FEVER 2.0 (2019)**
- Thorne, Vlachos et al. "The FEVER2.0 Shared Task." [ACL D19-6601](https://aclanthology.org/D19-6601/). Build-it / break-it / fix-it format; FEVER 2.0 adversarial dataset = 1,174 claims from breakers ([fever.ai adversarial dataset page](https://fever.ai/dataset/adversarial.html), [search summary](https://aclanthology.org/D19-6601/)). Few breaker teams (so conclusions are weak); mostly manually crafted attacks targeting suspected weaknesses.

**LIAR (2017)**
- Wang. "'Liar, Liar Pants on Fire': A New Benchmark Dataset for Fake News Detection." ACL 2017 short. [ACL P17-2067](https://aclanthology.org/P17-2067/), [arXiv 1705.00648](https://arxiv.org/abs/1705.00648). 12.8K (12,791) PolitiFact statements, six labels (pants-on-fire ... true). Original hybrid CNN with metadata: 0.277 accuracy; text-only DistilBERT macro-F1 0.2713 vs TF-IDF 0.2434 — [emergentmind-style secondary summary via search](https://www.emergentmind.com/topics/liar-benchmark) (secondary source; treat as indicative).
- Text-only models land in the 0.27-0.30 range; metadata (speaker, party, credit history) boosts accuracy but is not evidence-grounded, and credit-history counts include the current statement (label leakage) — [same secondary source](https://www.emergentmind.com/topics/liar-benchmark).

**MultiFC (2019)**
- Augenstein, Lioma, Wang, Chaves Lima, Hansen, Hansen, Simonsen. "MultiFC: A Real-World Multi-Domain Dataset for Evidence-Based Fact Checking of Claims." EMNLP-IJCNLP 2019. [ACL D19-1475](https://aclanthology.org/D19-1475/). 26 English fact-check sites, expert labels, best model Macro-F1 49.2%. ACL Anthology material is CC BY 4.0 (the paper; dataset licence not confirmed). Dataset size (~34.9K claims) not on the fetched page; HF mirror exists at [pszemraj/multi_fc](https://huggingface.co/datasets/pszemraj/multi_fc).

**FEVEROUS (2021)**
- Aly, Guo, Schlichtkrull, Thorne, Vlachos, Christodoulopoulos, Cocarascu, Mittal. "FEVEROUS: Fact Extraction and VERification Over Unstructured and Structured information." NeurIPS 2021 D&B. [arXiv 2106.05707](https://arxiv.org/abs/2106.05707). 87,026 claims, evidence from Wikipedia text and tables; baseline gets 18% FEVEROUS score.

**SciFact (2020) and successors**
- Wadden, Lin, Lo, Wang, van Zuylen, Cohan, Hajishirzi. "Fact or Fiction: Verifying Scientific Claims." EMNLP 2020. [arXiv 2004.14974](https://arxiv.org/abs/2004.14974). 1.4K expert-written claims with rationale-annotated abstracts; open access, code and leaderboard from AI2 ([GitHub allenai/scifact](https://github.com/allenai/scifact)).
- Wadden et al. "MultiVerS" (NAACL Findings 2022). [arXiv 2112.01640](https://arxiv.org/pdf/2112.01640). 72.5 F1 on SciFact test (abstract-level) and top-of-leaderboard systems within ~1.25 F1 — [search summary](https://github.com/dwadden/multivers).
- Wadden et al. "SciFact-Open." EMNLP Findings 2022. [arXiv 2210.13777](https://arxiv.org/abs/2210.13777). 500K-abstract corpus; systems lose at least 15 F1 vs the small-corpus setting.

**Climate-FEVER (2020)**
- Diggelmann, Boyd-Graber, Bulian, Ciaramita, Leippold. "CLIMATE-FEVER: A Dataset for Verification of Real-World Climate Claims." NeurIPS 2020 Climate Change AI workshop. [arXiv 2012.00614](https://arxiv.org/abs/2012.00614). 1,535 claims, 7,675 claim-evidence pairs (top-5 Wikipedia sentences each, up to 5 annotators, majority vote, ties become NEI) — [search result](https://arxiv.org/pdf/2012.00614). Original paper has no strong baseline numbers in the fetched abstract. Also used as BEIR retrieval task.

**AVeriTeC (2023-2025)**
- Schlichtkrull, Guo, Vlachos. "AVeriTeC: A Dataset for Real-world Claim Verification with Evidence from the Web." NeurIPS 2023 D&B. [arXiv 2305.13117](https://arxiv.org/abs/2305.13117). 4,568 claims from 50 fact-check orgs; 3,068 train / 500 dev / 1,000 test, chronological split; QA-pair evidence plus justification; labels Supported / Refuted / Conflicting Evidence-Cherrypicking / Not Enough Evidence; refuted ~56-62% of each split; kappa 0.619 (Randolph's free-marginal); licence CC-BY-NC-4.0 data, CC-BY-4.0 code — [arXiv HTML fetch](https://arxiv.org/html/2305.13117). Baseline: AVeriTeC score 0.21 (questions only) / 0.16 (questions+answers); veracity accuracy with gold evidence 0.49 — same source. The fetch also reported a claim-only accuracy of "0.03", which is implausible as a veracity accuracy; do not quote it without checking the paper.
- Schlichtkrull, Guo, Vlachos et al. "The Automated Verification of Textual Claims (AVeriTeC) Shared Task." FEVER 2024. [ACL 2024.fever-1.1](https://aclanthology.org/2024.fever-1.1/), [arXiv 2410.23850](https://arxiv.org/abs/2410.23850). 21 submissions, 18 beat baseline. Scores: TUDA_MAI 0.63, HUMANE 0.57, CTU AIC 0.50, Dunamu-ml 0.50, Papelo 0.48, baseline 0.11. Test expanded to 2,215 claims (1,000 original + 1,215 new; 5,783 total). Evidence matched via Hungarian METEOR with threshold 0.25 — [arXiv HTML fetch](https://arxiv.org/html/2410.23850).
- Rothermel, Braun, Rohrbach, Rohrbach. "InFact: A Strong Baseline for Automated Fact-Checking." FEVER 2024 (winner, GPT-4o, six-stage pipeline using the provided knowledge store, 63%). [ACL 2024.fever-1.12](https://aclanthology.org/2024.fever-1.12/).
- Yoon et al. "HerO at AVeriTeC: The Herd of Open Large Language Models for Verifying Real-World Claims." [arXiv 2410.12377](https://arxiv.org/abs/2410.12377) — open-LLM system, 2nd place (0.57 in the findings table, listed as HUMANE).
- Yoon, Jung, Yoon, Park. "Team HUMANE at AVeriTeC 2025: HerO 2 for Efficient Fact Verification." FEVER 2025. [arXiv 2507.11004](https://arxiv.org/abs/2507.11004). Second place in 2025, fastest of top three.
- "The 2nd Automated Verification of Textual Claims (AVeriTeC) Shared Task: Open-weights, Reproducible and Efficient Systems." FEVER 2025. [ACL 2025.fever-1.15](https://aclanthology.org/2025.fever-1.15/). 7 submissions, 6 beat baseline, winner CTU AIC at 33.17% AVeriTeC score; open-weights models only, single 23GB GPU, under one minute per claim.

**ClaimBuster**
- Hassan, Arslan, Li, Tremayne. "Toward Automated Fact-Checking: Detecting Check-worthy Factual Claims by ClaimBuster." KDD 2017. [ACM 10.1145/3097983.3098131](https://dl.acm.org/doi/10.1145/3097983.3098131). Check-worthiness classifier for political debates.
- Hassan, Zhang, Arslan, Caraballo et al. "ClaimBuster: The First-ever End-to-end Fact-checking System." PVLDB 10(7), 2017. [ACM 10.14778/3137765.3137815](https://dl.acm.org/doi/10.14778/3137765.3137815). Pipeline: claim monitor, spotter, matcher, checker, reporter.
- Numbers (F1 etc.) not retrieved — see Gaps. Related: Arslan et al. "A Benchmark Dataset of Check-worthy Factual Claims" (ICWSM 2020) was not verified in this session.

**CheckThat! lab (CLEF)**
- Alam et al. "The CLEF-2025 CheckThat! Lab: Subjectivity, Fact-Checking, Claim Normalization, and Retrieval." [arXiv 2503.14828](https://arxiv.org/abs/2503.14828). Tasks: subjectivity, claim normalization, numerical fact-checking, scientific web discourse; 20+ languages.
- "The CLEF-2024 CheckThat! Lab: Check-Worthiness, Subjectivity, Persuasion, Roles, Authorities, and Adversarial Robustness." ECIR 2024 / Springer [link](https://link.springer.com/chapter/10.1007/978-3-031-56069-9_62). Six tasks, 15 languages.
- "The CLEF-2026 CheckThat! Lab: Advancing Multilingual Fact-Checking." [arXiv 2602.09516](https://arxiv.org/abs/2602.09516). Tasks: scientific web claim source retrieval, numerical/temporal claim fact-checking with reasoning, full fact-check article generation.
- Task-level leaderboard numbers were not retrieved.

**Cross-benchmark and recent evaluation**
- Usmanova, Iklassov, Leippold, Usbeck. "How Robust Are Automated Fact-Checking Systems? A Cross-Benchmark Evaluation." [arXiv 2608.25934](https://arxiv.org/abs/2608.25934). Nine models, four datasets (SciFact, ClimateCheck, AVeriTeC 2025, others): best macro-F1 0.70 on SciFact vs 0.31 on ClimateCheck; gold evidence improves veracity accuracy 14-22 points; Conflicting Evidence is universally hard; NEI over-prediction is the main LLM error; annotation issues cause most failures, so gaps under 5 points may reflect label noise.
- Wang et al. "Fact-Checking with Large Language Models via Probabilistic Certainty and Consistency." [arXiv 2601.02574](https://arxiv.org/abs/2601.02574). Confidence-guided adaptive retrieval across three benchmarks (which three not stated in the fetch).

### Inferences
- For a RAG fact-checker, report AVeriTeC score and label accuracy separately; the retrieval bottleneck means label accuracy with gold evidence is the upper bound.
- LIAR text-only ~0.27-0.30 is the realistic floor-level comparison; anything far above that likely uses metadata.
- Because AVeriTeC 2024 winners used GPT-4o while 2025 capped at open-weights / 23GB GPU, the 0.33 (2025) is the more relevant reference for a low-resource project, though the knowledge-store and test conditions differ between years.

### Gaps
- Official label accuracy per team for AVeriTeC 2024/2025 (only AVeriTeC scores found; PDFs could not be parsed).
- Current FEVER leaderboard SOTA (post-2019) and FEVER 1.0 baseline metric attribution not confirmed.
- ClaimBuster and CheckThat! numeric results, MultiFC claim count, Climate-FEVER baseline accuracies not retrieved.
- Licence for FEVER, LIAR, MultiFC, SciFact, Climate-FEVER, FEVEROUS data files not confirmed from official pages.

## 2. Which datasets are best for a CPU-only student project and why?

### Takeaway
Best fit: AVeriTeC (real-world, small: 3,068 train / 500 dev claims, matches a RAG plus audit design, with a precompiled knowledge store) used with small retrievers and API or small-LM verdicts; SciFact (1.4K claims, small abstract corpus) and Climate-FEVER (1,535 claims) as cheap secondary domains; LIAR as a cheap bias/calibration playground. Avoid full FEVER/FEVEROUS corpora (Wikipedia-scale retrieval) on CPU.

### Cited Findings
- AVeriTeC: 4,568 claims total, evidence is QA pairs, licence CC-BY-NC-4.0 (non-commercial, fine for a student project) — [arXiv 2305.13117](https://arxiv.org/html/2305.13117).
- 2025 task set a precedent for efficiency: open-weights models on a 23GB GPU, under one minute per claim — [ACL 2025.fever-1.15](https://aclanthology.org/2025.fever-1.15/). A CPU-only project cannot match that runtime for large LLMs, so use quantised small models or hosted APIs.
- SciFact: 1.4K claims; open access with GitHub release — [arXiv 2004.14974](https://arxiv.org/abs/2004.14974). Corpus of abstracts is small (SciFact-Open expands to 500K abstracts, much heavier) — [arXiv 2210.13777](https://arxiv.org/abs/2210.13777).
- Climate-FEVER: 1,535 claims, 7,675 pairs with pre-retrieved evidence, so verification can be tested without retrieval — [arXiv 2012.00614](https://arxiv.org/pdf/2012.00614).
- LIAR: 12.8K short statements, metadata available, supports subgroup analysis by speaker/party/topic — [ACL P17-2067](https://aclanthology.org/P17-2067/).

### Inferences
- A sensible CPU-feasible stack: AVeriTeC dev (500 claims) for headline evaluation, Climate-FEVER and SciFact for domain-shift checks, LIAR for subgroup/calibration audit (no retrieval needed).
- FEVER and FEVEROUS need Wikipedia-scale indexing; feasible only with the shipped sentence subsets or sampling.

### Gaps
- Actual CPU runtimes/memory for embedding the AVeriTeC knowledge store were not found.
- Knowledge store download size not confirmed.

## 3. What known artifacts, label noise, political/topic bias, or leakage issues exist?

### Takeaway
FEVER has strong claim-only artifacts; real-world datasets suffer from leaked fact-check articles and temporal leakage, label noise (SciFact gold errors), and metadata shortcuts (LIAR). Bias analyses by subgroup exist only sporadically (geographic, political-connotation) and not as part of standard benchmarks.

### Cited Findings
- Claim-only classifiers are competitive with evidence-aware FEVER systems; the top FEVER shared-task system gets 81.8% on original but 58.7% on the Symmetric test set — Schuster, Shah, Yeo, Filizzola, Santus, Barzilay. "Towards Debiasing Fact Verification Models." EMNLP 2019. [arXiv 1908.05267](https://arxiv.org/abs/1908.05267); data at [GitHub TalSchuster/FeverSymmetric](https://github.com/TalSchuster/FeverSymmetric). Cues are idiosyncratic claim phrases (e.g. negation); they propose reweighting regularisation.
- Counterfactual debiasing follow-up: "Counterfactual Debiasing for Fact Verification." ACL 2023. [ACL 2023.acl-long.374](https://aclanthology.org/2023.acl-long.374.pdf).
- FEVER-2.0 breakers found systematic weaknesses mostly by hand-crafted attacks — [ACL D19-6601](https://aclanthology.org/D19-6601/). Survey: "Adversarial Attacks Against Automated Fact-Checking: A Survey." [arXiv 2509.08463](https://arxiv.org/abs/2509.08463).
- Leaked evidence: Glockner, Hou, Gurevych. "Missing Counter-Evidence Renders NLP Fact-Checking Unrealistic for Misinformation." EMNLP 2022. [ACL 2022.emnlp-main.397](https://aclanthology.org/2022.emnlp-main.397/). Existing datasets fail both criteria (evidence sufficient to refute; not leaked from fact-checking articles); models trained on them rely on leaked evidence.
- AVeriTeC addresses temporal leakage by requiring evidence published before the claim and chronological splits — [arXiv HTML](https://arxiv.org/html/2305.13117). But shared-task organisers found date-formatting errors let post-claim fact-check articles enter the knowledge store, and the scraper failed to extract text for 297 of 500 dev examples — [arXiv 2410.23850 HTML](https://arxiv.org/html/2410.23850). Hungarian METEOR correlates poorly with human evidence judgments — same source.
- Lu and Setiawan. "No Hindsight for LLM Fact-Checkers: Measuring Leakage Channels in Misinformation Detection." [arXiv 2610.04888](https://arxiv.org/abs/2610.04888). Parametric leakage (memorised outcomes) substantial on AVeriTeC and QuanTemp++; post-claim evidence inflates zero-shot AVeriTeC accuracy by 6.3 points (negligible on QuanTemp++). Very recent; only the abstract-level summary was read.
- Label noise: Sylvestre. "Gold Label Errors in the SciFact Benchmark: An LLM-Assisted Annotation Audit." BioNLP 2026. [ACL 2026.bionlp-1.9](https://aclanthology.org/2026.bionlp-1.9/). 11 errors in 209 audited dev pairs (5.3%), 13 in 564 train pairs (2.3%); correcting raises binary macro-F1 by 1.7-3.8 points. Related: "Are LLMs Better than Reported? Detecting Label Errors..." [arXiv 2410.18889](https://arxiv.org/abs/2410.18889).
- Cross-benchmark noise: annotation issues explain most failures; margins under 5 points may be noise — [arXiv 2608.25934](https://arxiv.org/abs/2608.25934).
- LIAR metadata (speaker, party, credit history) shortcut and unwanted party/group bias — [secondary summary](https://www.emergentmind.com/topics/liar-benchmark). Also Pelrine et al. "Towards Reliable Misinformation Mitigation: Generalization, Uncertainty, and GPT-4" ([arXiv 2305.14928](https://arxiv.org/abs/2305.14928)): GPT-4 and RoBERTa-large fail differently across datasets; uncertainty-based identification of claims lacking context improves performance; releases LIAR-New (CC BY 4.0) with "Possibility" labels for context sufficiency.
- Political/subgroup bias: Coelho et al. "Understanding Inequality of LLM Fact-Checking over Geographic Regions" ([arXiv 2503.22877](https://arxiv.org/abs/2503.22877)): 600 statements, six regions; Global North statements verified better than Global South, gap larger with Wikipedia-agent. PolBiX ([arXiv 2509.15335](https://arxiv.org/abs/2509.15335)): euphemism/dysphemism minimal pairs in German claims; judgmental wording affects truthfulness judgments more than political leaning, and objectivity prompts do not fix it. "Independent fact-checking organizations exhibit a departure from political neutrality" ([arXiv 2407.19498](https://arxiv.org/abs/2407.19498)) — relevant because all real-world labels come from fact-checkers (abstract not read in detail).
- Class skew: AVeriTeC refuted claims dominate (~56-62%), reflecting journalist selection — [arXiv HTML](https://arxiv.org/html/2305.13117).
- Conflicting-Evidence/Cherrypicking is the hardest label across benchmarks — [arXiv 2608.25934](https://arxiv.org/abs/2608.25934).

### Inferences
- A bias/calibration audit layer is novel relative to the benchmark papers: none of the dataset papers report calibration (ECE) or subgroup breakdowns by topic/party/region as standard.
- Practical audit design: (1) claim-only baseline on every dataset, (2) Symmetric/ minimal-pair tests, (3) evidence-date filtering, (4) memorisation probe on pre-cutoff vs post-cutoff claims, (5) per-label and per-topic/speaker calibration on LIAR, AVeriTeC.
- LLM knowledge cutoff vs claim date is the key leakage control for AVeriTeC (claims 2015-2022ish; exact date range not confirmed).

### Gaps
- No source found giving ECE/calibration numbers on AVeriTeC or FEVER for RAG fact-checkers.
- No topic/party-level breakdown for AVeriTeC or MultiFC found.
- Claim-only baseline values for AVeriTeC and Climate-FEVER not confirmed.
- Date range of AVeriTeC claims not confirmed.
- Search-engine-based summaries of Hungarian-METEOR issue and 2610.04888/2608.25934 rely on fetch-tool summaries; read full papers before citing specifics.
