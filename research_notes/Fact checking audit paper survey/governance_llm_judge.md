# Governance/documentation frameworks and LLM-as-judge evaluation for an audit layer (as of 6 Oct 2026)

Verification note: article content below was fetched from artificialintelligenceact.eu (Future of Life Institute's article-by-article mirror of the Regulation, which was updated to reflect the 2026 omnibus). EUR-Lex pages returned empty content to my fetcher, so EUR-Lex links are given as official canonical links but I could NOT open them myself. Quote final wording from EUR-Lex before publishing. Official ELI for the AI Act: https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng (OJ L, 12 July 2024; not re-verified by me, from background knowledge).

## 1. What exactly does the EU AI Act require that a project audit report can map to (articles, dates, EUR-Lex)?

### Takeaway
A fact-checking/misinformation tool is most likely NOT high-risk by default (not an Annex III use case unless deployed in listed areas), so the binding items are Art. 50 transparency (applies from 2 Aug 2026, with 2(2) marking grace to 2 Dec 2026), Art. 4 AI literacy, and (if a GPAI model is provided) Art. 53. Arts. 9-15 are still the best-practice yardstick for an audit report, and become binding only if the system is classified high-risk (now from 2 Dec 2027 for Annex III). The Digital Omnibus on AI, Regulation (EU) 2026/1744, is law (in force 27 Jul 2026) and changed these dates.

### Cited Findings
**Legal instruments and links**
- AI Act = Regulation (EU) 2024/1689; EUR-Lex ELI [eur-lex.europa.eu/eli/reg/2024/1689/oj/eng](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng) (I could not retrieve the page content; link from background knowledge).
- Digital Omnibus on AI = Regulation (EU) 2026/1744 of 8 July 2026 amending Regulations (EU) 2024/1689, 2018/1139 and 2023/1230; published in the OJ 24 July 2026; in force 27 July 2026; EUR-Lex: [eur-lex.europa.eu/eli/reg/2026/1744/oj/eng](https://eur-lex.europa.eu/eli/reg/2026/1744/oj/eng) (link surfaced in search results; title/dates per [secondary summary](https://lawandtechnology.eu/en/digital-omnibus-on-ai-official-journal-regulation-2026-1744/) and [EP Legislative Train](https://www.europarl.europa.eu/legislative-train/package-digital-package/file-digital-omnibus-on-ai)).
- Omnibus timeline: Commission proposal 19 Nov 2025; trilogue agreement 7 May 2026; EP plenary 16 Jun 2026; Council adoption 29 Jun 2026; signed 8 Jul 2026; procedure 2025/0359(COD) — [EP Legislative Train](https://www.europarl.europa.eu/legislative-train/package-digital-package/file-digital-omnibus-on-ai).

**Application dates (Art. 113, as amended)**
- Original general application date: 2 Aug 2026. Chapters I-II (incl. Art. 4 AI literacy, Art. 5 prohibitions) since 2 Feb 2025; GPAI (Chapter V), governance, penalties (Ch. XII) from 2 Aug 2025; high-risk Chapter III Sections 1-3 now 2 Dec 2027 (Annex III / Art. 6(2)) and 2 Aug 2028 (Annex I / Art. 6(1)) — [Art. 113 (artificialintelligenceact.eu)](https://artificialintelligenceact.eu/article/113/); confirmed by [Gibson Dunn](https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/) and [Morgan Lewis](https://www.morganlewis.com/pubs/2026/06/eu-approves-delays-and-other-amendments-to-certain-eu-ai-act-obligations-what-businesses-should-know).
- Previously: high-risk Annex III was 2 Aug 2026 and Annex I 2 Aug 2027; the omnibus moved them 16 and 12 months respectively — [Morgan Lewis](https://www.morganlewis.com/pubs/2026/06/eu-approves-delays-and-other-amendments-to-certain-eu-ai-act-obligations-what-businesses-should-know).
- Art. 50 stays at 2 Aug 2026, with a four-month grace period (to 2 Dec 2026) for the Art. 50(2) machine-readable marking duty for systems already on the market before 2 Aug 2026 — [Gibson Dunn](https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/). (Morgan Lewis and a Usercentrics summary describe it more loosely as the watermarking date moving to 2 Dec 2026; treat Gibson Dunn's "pre-existing systems" qualification as the more precise reading and check the text of Reg. 2026/1744.)
- Other omnibus changes: Art. 4 AI literacy softened from ensuring sufficient literacy to "take measures to support" it (still applies from 2 Feb 2025) — [regulation-ai.eu](https://www.regulation-ai.eu/en/changes/); bias-detection legal basis for special-category data extended to all AI systems and GPAI models; AI Office exclusive competence over AI systems built on the same provider's GPAI model; regulatory sandbox deadline to 2 Aug 2027; simplified regime extended to mid-caps (<=750 staff) — [Gibson Dunn](https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/), [Morgan Lewis](https://www.morganlewis.com/pubs/2026/06/eu-approves-delays-and-other-amendments-to-certain-eu-ai-act-obligations-what-businesses-should-know).
- New Art. 5 prohibition on systems generating non-consensual intimate imagery/CSAM, transitional to 2 Dec 2026 — Gibson Dunn and Morgan Lewis (above); CONFLICT: [regulation-ai.eu](https://www.regulation-ai.eu/en/changes/) says Art. 5 had no change. Not relevant to fact-checking; flag only.

**Art. 50 (transparency) — [Art. 50](https://artificialintelligenceact.eu/article/50/)**
- 50(1): providers must design systems that interact directly with people so they are informed they interact with AI, unless obvious.
- 50(2): providers of systems generating synthetic audio, image, video or text must mark outputs in a machine-readable format and detectable as artificially generated/manipulated (technically feasible, state of the art); exemption for assistive editing.
- 50(3): deployers of emotion recognition/biometric categorisation must inform exposed persons.
- 50(4): deployers must disclose deepfakes and AI-generated/manipulated text published to inform the public on matters of public interest; exemptions include law enforcement, evident artistic work, and text that underwent human review/editorial control with editorial responsibility.
- 50(5): information must be clear and distinguishable at latest at first interaction/exposure; accessibility. 50(6): does not replace Chapter III or other law. 50(7): Commission encourages codes of practice.
- Commission published the final Code of Practice on marking and labelling AI-generated content on 10 Jun 2026 (voluntary); recommends at least two layers of machine-readable marking; deployer section on labelling; the Commission will also issue Art. 50 guidelines — [Jones Day](https://www.jonesday.com/en/insights/2026/06/european-commission-publishes-final-code-of-practice-on-marking-and-labelling-aigenerated-content).
- Art. 50 not textually amended by the omnibus — [regulation-ai.eu](https://www.regulation-ai.eu/en/changes/).

**Art. 15 (accuracy, robustness, cybersecurity; high-risk only) — [Art. 15](https://artificialintelligenceact.eu/article/15/)**
- 15(1): appropriate level of accuracy, robustness, cybersecurity, consistent throughout lifecycle. 15(2): Commission to encourage benchmarks and measurement methodologies. 15(3): accuracy levels and relevant metrics declared in instructions for use. 15(4): resilience to errors/faults/inconsistencies; fail-safe/backup; for systems that continue learning, avoid biased outputs feeding back into inputs (feedback loops). 15(5): resilience to unauthorised third-party attempts to alter use/outputs/performance; AI-specific vulnerabilities (data poisoning, model poisoning, adversarial examples/model evasion, confidentiality attacks, model flaws).

**Other high-risk-chapter articles useful as audit mapping (all binding for high-risk only)**
- Art. 13: transparency/instructions for use incl. accuracy level and metrics, known circumstances affecting accuracy, foreseeable misuse, performance on specific groups, input data specs, human oversight, log mechanisms — [Art. 13](https://artificialintelligenceact.eu/article/13/).
- Art. 12: automatic event logging over system lifetime for traceability, risk identification, post-market monitoring — [Art. 12](https://artificialintelligenceact.eu/article/12/). (Arts. 9 risk management, 10 data governance, 11 technical documentation/Annex IV, 14 human oversight: not fetched by me; numbering from background knowledge, verify on EUR-Lex.)
- Art. 6(3)-(4): an Annex III system is not high-risk if no significant risk and it meets a derogation (narrow procedural task, improves prior human activity, detects patterns without replacing review, preparatory task), but profiling of natural persons is always high-risk; provider must document the assessment before market placement and register (Art. 49(2)) — [Art. 6](https://artificialintelligenceact.eu/article/6/).
- Annex III areas: biometrics; critical infrastructure; education; employment; essential services; law enforcement; migration/border; justice and democratic processes (judicial assistance; influencing elections/voting behaviour) — [Annex III](https://artificialintelligenceact.eu/annex/3/). A fact-checker used by a court, or one directed at influencing voting behaviour, could touch point 8; a general misinformation-flagging tool normally does not (inference, not legal advice).
- Art. 53 (GPAI model providers): Annex XI technical documentation; Annex XII info to downstream providers on capabilities and limitations; copyright policy; public training-content summary; open-source exemptions do not cover systemic-risk models; codes of practice/standards as compliance route — [Art. 53](https://artificialintelligenceact.eu/article/53/). Applies since 2 Aug 2025 (Art. 113 above). A project that only deploys a third-party LLM is a downstream provider/deployer and should request Annex XII information.
- Art. 99 fines: up to EUR 35M/7% (Art. 5), EUR 15M/3% (operator obligations incl. transparency Art. 50), EUR 7.5M/1% (incorrect info to authorities); lower caps for SMEs — [Art. 99](https://artificialintelligenceact.eu/article/99/). (GPAI fines are under Art. 101, not verified.)

### Inferences
- Audit-report mapping table proposal: Art. 50(1) -> UI disclosure that outputs are AI; 50(2) -> machine-readable marking of generated verdicts/explanations (metadata/watermark); 50(4) -> labelling when AI-generated text on public-interest matters is published, unless human editorial review is documented; Art. 13/15(3) -> publish accuracy metrics (e.g., judge-vs-human kappa, precision/recall of verdicts) and known failure conditions; Art. 12 -> logs of claims, evidence, judge scores and model versions; Art. 15(4) feedback loops -> avoid retraining on own judge outputs; Art. 15(5) -> prompt-injection/poisoning tests of retrieved evidence; Art. 6(3)/(4) -> a documented classification memo.
- Reporting should say "voluntary alignment with Arts. 9-15" rather than "compliant" unless high-risk status applies.

### Gaps
- EUR-Lex text of Reg. 2024/1689 and 2026/1744 could not be opened; consolidated post-omnibus text not verified directly; article-level citations rely on artificialintelligenceact.eu plus law-firm summaries.
- Arts. 9, 10, 11, 14, 72, 73, 101 and Annex IV not fetched. Commission Art. 50 guidelines status unknown. Whether fact-checking is high-risk is a legal-classification question not answered by any source I found.

## 2. Documentation frameworks: Model Cards, Datasheets for Datasets, NIST AI RMF

### Takeaway
Model Cards and Datasheets are the standard artefacts for documenting a model and its data; NIST AI RMF (+ GenAI Profile) is the standard voluntary risk-management structure. All three map naturally onto Art. 11/13/53 documentation and an audit report's structure.

### Cited Findings
- Mitchell, Wu, Zaldivar, Barnes, Vasserman, Hutchinson, Spitzer, Raji, Gebru. "Model Cards for Model Reporting." FAT* '19 (ACM FAccT), Jan 2019. arXiv:1810.03993. One-liner: short documents accompanying models reporting performance across demographic/intersectional groups and conditions, intended use and evaluation methodology — [arXiv](https://arxiv.org/abs/1810.03993).
- Gebru, Morgenstern, Vecchione, Vaughan, Wallach, Daume III, Crawford. "Datasheets for Datasets." Communications of the ACM, Dec 2021 (arXiv:1803.09010, first posted 2018). One-liner: question-based documentation for datasets (motivation, composition, collection, uses), modelled on electronics datasheets — [arXiv](https://arxiv.org/abs/1803.09010).
- NIST AI RMF 1.0 (NIST AI 100-1), released 26 Jan 2023; four functions (Govern, Map, Measure, Manage; the NIST page lists them in a different order); Playbook and AI Resource Center at airc.nist.gov; Generative AI Profile NIST AI 600-1 released 26 Jul 2024; AI RMF revision under way per the White House AI Action Plan; 7 Apr 2026 concept note for a Critical Infrastructure profile — [NIST AI RMF page](https://www.nist.gov/itl/ai-risk-management-framework).

### Inferences
- Use a Model Card for the judge model and for the verdict pipeline (intended use, metrics, subgroup performance, limitations); a Datasheet for the claim/evidence evaluation set (provenance, labelling process, annotator agreement); NIST Measure function for the LLM-judge validation plan; GenAI Profile for hallucination/"confabulation" and information-integrity risks. These documents double as Art. 11/13/Annex XII evidence.

### Gaps
- Did not verify the NIST AI 600-1 risk category list or Govern/Map/Measure/Manage subcategory IDs. No source found comparing model-card fields to AI Act Annex IV field by field (not searched deeply). Hugging Face model-card templates not checked.

## 3. When is LLM-as-judge reliable, and how to validate it (human agreement, kappa)?

### Takeaway
LLM judges reach roughly human-human agreement on general chat preference with strong models (>80%), but are weaker on expert domains, absolute scoring, and subtle properties, and carry position, verbosity/length, and self-preference biases. Validate on your own labelled sample with chance-corrected agreement and bias probes before relying on it.

### Cited Findings
- Zheng et al. "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena." NeurIPS 2023 Datasets & Benchmarks. GPT-4 judge achieves over 80% agreement with controlled and crowdsourced human preferences; names position, verbosity and self-enhancement bias; releases MT-Bench with 3K expert votes and 30K Arena conversations — [arXiv:2306.05685](https://arxiv.org/abs/2306.05685).
- Chiang & Lee, "Can Large Language Models Be an Alternative to Human Evaluations?" ACL 2023: LLM ratings agree with expert preferences and are stable across instruction formats — [arXiv:2305.01937](https://arxiv.org/abs/2305.01937).
- G-Eval: Liu et al., EMNLP 2023, CoT + form-filling; Spearman 0.514 with humans on summarisation; authors note bias toward LLM-generated text — [arXiv:2303.16634](https://arxiv.org/abs/2303.16634).
- Position bias: Wang et al. 2023 show rankings can be flipped by reordering; propose multiple evidence calibration, balanced position calibration, human-in-the-loop — [arXiv:2305.17926](https://arxiv.org/abs/2305.17926). Shi et al. (AACL-IJCNLP 2025): 15 judges, ~150,000 instances; bias not random, varies by judge/task; metrics repetition stability, position consistency, preference fairness — [arXiv:2406.07791](https://arxiv.org/abs/2406.07791).
- Verbosity/length: Dubois et al., Length-Controlled AlpacaEval, COLM 2024; length control raised correlation with Chatbot Arena from 0.94 to 0.98 — [arXiv:2404.04475](https://arxiv.org/abs/2404.04475).
- Self-preference: Panickssery, Bowman, Feng 2024: judges recognise own outputs, linear relation between self-recognition and self-preference — [arXiv:2404.13076](https://arxiv.org/abs/2404.13076); Wataoka et al. (NeurIPS 2024 workshop): bias linked to low perplexity, not only authorship — [arXiv:2410.21819](https://arxiv.org/abs/2410.21819).
- Broader bias taxonomy: Ye et al. "Justice or Prejudice?" CALM framework, 12 biases — [arXiv:2410.02736](https://arxiv.org/abs/2410.02736).
- Reliability studies: Thakur et al. "Judging the Judges" (GEM 2025, ACL): only the best/largest models align reasonably with humans, judges rank models better than they score absolutely, lenient — [arXiv:2406.12624](https://arxiv.org/abs/2406.12624). Bavaresco et al. (ACL 2025), JUDGE-BENCH, 20 datasets, 11 LLMs: substantial variability by property and annotator expertise; validate against humans first — [arXiv:2406.18403](https://arxiv.org/abs/2406.18403). Szymanski et al.: domain experts agreed with LLM judges 68% (dietetics) and 64% (mental health) — [arXiv:2410.20266](https://arxiv.org/abs/2410.20266).
- Critique in IR: Clarke & Dietz argue LLM relevance judgments can't replace humans (gaming, circularity, "narcissism") — [arXiv:2412.17156](https://arxiv.org/abs/2412.17156).
- Survey: Gu et al., "A Survey on LLM-as-a-Judge" — [arXiv:2411.15594](https://arxiv.org/abs/2411.15594).
- Fact-level evaluation: FActScore (Min et al., EMNLP 2023) decomposes text into atomic facts, scores the share supported by a knowledge source; automated estimator <2% error vs human — [arXiv:2305.14251](https://arxiv.org/abs/2305.14251).

### Inferences
- Validation protocol: (1) human-label a stratified sample (e.g., 100-300 claims) by two annotators; report inter-annotator Cohen's/Fleiss' kappa or Krippendorff alpha; (2) report judge-vs-human kappa (not just raw percent agreement, since class imbalance inflates it; Thakur et al. also argue for chance-corrected metrics, from my reading of the abstract only), confusion matrix, per-class precision/recall; (3) swap-order test and report position consistency; (4) length-controlled analysis; (5) use a judge from a different family than the generator; (6) temperature 0 plus repeated runs; (7) re-validate on model/version change; (8) bootstrap CIs. Landis-Koch kappa bands are conventional but arbitrary; no source fetched.
- Unreliable zones: expert/health content, fine-grained absolute scores, judge = generator family, adversarial inputs.

### Gaps
- Did not find a 2025-26 paper giving a definitive kappa threshold for acceptance. MT-Bench per-category agreement/kappa figures not extracted. Prompt-injection attacks on judges, judge distillation (e.g., Prometheus, JudgeLM) and "LLM-as-judge for fact-checking" specifically were not searched.

## 4. RAG evaluation frameworks and which run cheaply

### Takeaway
RAGAS, ARES, RAGChecker and FActScore cover faithfulness/groundedness and retrieval quality; most RAGAS metrics need LLM calls (cost scales with samples x metrics), but they can use a local/open-weight or small judge.

### Cited Findings
- RAGAS: Es, James, Espinosa-Anke, Schockaert. "Ragas: Automated Evaluation of Retrieval Augmented Generation" (arXiv:2309.15217; EACL 2024 demo track per background knowledge, not shown on the arXiv page I fetched); reference-free evaluation of retrieval relevance, faithfulness, generation quality — [arXiv](https://arxiv.org/abs/2309.15217). Docs list Faithfulness, Context Precision, Context Recall, Response Relevancy, Context Entities Recall, Noise Sensitivity; LLM-based metrics use one or more LLM calls; context recall needs reference answers — [Ragas docs](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/).
- ARES: Saad-Falcon, Khattab, Potts, Zaharia, NAACL 2024; fine-tunes lightweight LM judges on synthetic data, prediction-powered inference with few hundred human labels; context relevance, answer faithfulness, answer relevance — [arXiv:2311.09476](https://arxiv.org/abs/2311.09476). Cheap at inference after one-time training.
- RAGChecker: Ru et al. 2024, claim-level diagnostics for retrieval and generation modules; meta-evaluated vs human judgements — [arXiv:2408.08067](https://arxiv.org/abs/2408.08067).
- FActScore (above) is open source, pip-installable.

### Inferences
- Cheapest viable setup: RAGAS faithfulness + context precision with a small/open-weight or cheap-API judge on a sampled subset; ARES-style small fine-tuned judge for scale; validate any of them with the Section 3 protocol. Not verified: DeepEval, TruLens, and ARES/RAGChecker compute cost figures; HHEM/NLI-based (non-LLM) cheap alternatives not researched.

### Gaps
- No cost/latency benchmark of RAG frameworks found. No 2025-26 critique specific to RAGAS reliability fetched. Unfetched candidates worth checking: DeepEval, TruLens, TRACe/RAGBench, HHEM.
