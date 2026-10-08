# RAG, LLM claim verification, and citation attribution/faithfulness: curated papers

Method note: each paper below had its arXiv/ACL/HF page fetched in this session and the title, authors and venue confirmed from that page. Numbers are included only when they appeared in a fetched page or search result. Where I lack a number, it is listed under Gaps. "Not verified" marks anything from memory.

## What architecture patterns work best for claim verification with cited evidence?

### Takeaway
The pattern that recurs is: decompose into atomic claims, generate queries, retrieve (BM25 and/or dense), verify each claim against its evidence (LLM or small NLI-style verifier), then aggregate with a justification and evidence pointers. Iterative, confidence-gated retrieval (FIRE) cuts cost with no accuracy loss. On AVeriTeC the best systems retrieve evidence as question-answer pairs.

### Cited Findings
- RAG (Lewis et al., NeurIPS 2020): a seq2seq generator paired with a dense Wikipedia index via a neural retriever. It reached SOTA on three open-domain QA benchmarks and offers interpretable sources. Foundational; no claim-level audit. — [arXiv 2005.11401](https://arxiv.org/abs/2005.11401)
- Self-RAG (Asai, Wu, Wang, Sil, Hajishirzi; arXiv Oct 2023, ICLR 2024 per my memory, not verified in fetch): trains 7B and 13B LMs to retrieve on demand and critique with reflection tokens. The abstract says it outperforms ChatGPT and retrieval-augmented Llama2 on QA, reasoning, fact verification and long-form citation precision. 7B/13B models need a GPU; not CPU-friendly unless quantised. — [arXiv 2310.11511](https://arxiv.org/abs/2310.11511)
- FActScore (Min et al., EMNLP 2023): decomposes long-form text into atomic facts and reports the fraction supported by a knowledge source. ChatGPT scored 58% on biographies. The automatic estimator has under 2% error versus humans and was run over 6,500 generations. pip package available. — [arXiv 2305.14251](https://arxiv.org/abs/2305.14251)
- SAFE / LongFact (Wei et al., NeurIPS 2024): LLM agent splits a response into facts and checks each with Google Search. Agrees with crowdworkers on 72% of ~16k facts. On 100 sampled disagreements SAFE was right 76% of the time. About 20x cheaper than human annotation. Requires a paid LLM and search API. — [arXiv 2403.18802](https://arxiv.org/abs/2403.18802)
- FacTool (Chern et al., 2023): tool-augmented factuality pipeline covering knowledge QA, code, math and scientific literature. Code and ChatGPT plugin released. — [arXiv 2307.13528](https://arxiv.org/abs/2307.13528)
- ProgramFC (Pan et al., ACL 2023): LLM writes a reasoning program that decomposes a complex claim into sub-tasks handled by a shared function library. Gives an explicit, inspectable reasoning trace, which suits an audit log. Outperformed 7 baselines on two datasets. — [arXiv 2305.12744](https://arxiv.org/abs/2305.12744)
- HiSS (Zhang & Gao, AACL 2023): hierarchical step-by-step prompting. Splits a claim into subclaims and verifies each via question-answering steps. Beat supervised and few-shot baselines on two news-claim datasets. — [arXiv 2310.00305](https://arxiv.org/abs/2310.00305)
- FIRE (Xie et al., Findings NAACL 2025): iterative retrieve-or-answer agent. Accuracy comparable to or slightly better than competing frameworks. LLM cost about 7.6x lower and search cost about 16.5x lower on average. — [arXiv 2411.00784](https://arxiv.org/abs/2411.00784)
- Loki (Li, Nakov, Baldwin et al., Oct 2024): open-source (MIT) 5-step pipeline of decompose, check-worthiness, query generation, retrieval and verification. Human-in-the-loop design. — [arXiv 2410.01794](https://arxiv.org/abs/2410.01794)
- OpenFactCheck (Iqbal et al., EMNLP 2024 demos): three modules (ResponseEval, LLMEval, CheckerEval) to evaluate fact-checkers themselves. Useful for benchmarking your own pipeline. — [arXiv 2408.11832](https://arxiv.org/abs/2408.11832)
- RARR (Gao et al., ACL 2023): researches claims with search, then post-edits unsupported text. Attribution is added after generation (post-hoc). — [arXiv 2210.08726](https://arxiv.org/abs/2210.08726)
- AVeriTeC (Schlichtkrull, Guo, Vlachos, NeurIPS 2023 D&B): 4,568 real claims from 50 fact-checking organisations. Question-answer evidence from the web, textual justifications, inter-annotator kappa 0.619. — [arXiv 2305.13117](https://arxiv.org/abs/2305.13117)
- AVeriTeC 2024 shared task: 21 teams, 18 beat the baseline. Winner TUDA_MAI scored 63%, using gpt-4o. The score requires both a correct verdict and evidence passing a quality threshold. — [arXiv 2410.23850](https://arxiv.org/abs/2410.23850); winner details via [search summary](https://aclanthology.org/2024.fever-1.1/)
- HerO (Yoon et al., FEVER 2024): open LLMs only; AVeriTeC score 0.57, 2nd place. Best open-source system of that year. — [arXiv 2410.12377](https://arxiv.org/abs/2410.12377)
- HerO 2 (Yoon et al., FEVER @ ACL 2025): document summarisation, answer reformulation, post-training quantisation, updated backbones. 2nd place on the leaderboard and the fastest of the top three. — [arXiv 2507.11004](https://arxiv.org/abs/2507.11004)

### Inferences
- A defensible audit layer logs, per atomic claim: the query, retrieved passages with IDs, a verifier score, a verdict and a justification. ProgramFC, Loki and AVeriTeC all produce these artefacts.
- Use FIRE-style early stopping and a small verifier first, escalating to an LLM only for low-confidence claims, to keep cost low.

### Gaps
- I did not retrieve per-component ablations for AVeriTeC systems (BM25 vs dense, reranker, model size), so which retrieval choice matters most there is unconfirmed.
- Self-RAG headline numbers were not fetched.
- I found no first-hand numbers for the HerO 2 runtime or hardware.

## How is citation faithfulness / attribution measured, and with which tools (cheap enough for CPU)?

### Takeaway
Attribution is measured as "does the cited passage entail the statement", via human AIS annotation or NLI/alignment models as proxies. ALCE standardised this for citations: citation recall and precision judged by an NLI model. Recent work argues that entailment-based "correctness" is not the same as causal "faithfulness".

### Cited Findings
- AIS (Rashkin et al.): defines Attributable to Identified Sources with a two-stage human annotation pipeline, validated on conversational QA, summarisation and table-to-text. The protocol is the gold standard that automatic metrics approximate. — [arXiv 2112.12870](https://arxiv.org/abs/2112.12870)
- Attributed QA (Bohnet et al., 2022): reproducible evaluation setup for attributed LLMs. Identifies an automatic metric that correlates well with human judgments. — [arXiv 2212.08037](https://arxiv.org/abs/2212.08037)
- ALCE (Gao, Yen, Yu, Chen, EMNLP 2023): first benchmark for automatic LLM citation evaluation. Measures fluency, correctness and citation quality. On ELI5 even the best models lack complete citation support 50% of the time. Code at princeton-nlp/ALCE. — [arXiv 2305.14627](https://arxiv.org/abs/2305.14627)
- TRUE (Honovich et al., NAACL 2022): meta-evaluation of factual-consistency metrics across 11 datasets. Large-scale NLI and QG-QA methods give strong, complementary results. — [arXiv 2204.04991](https://arxiv.org/abs/2204.04991)
- AlignScore (Zha et al., ACL 2023): 355M-parameter unified alignment function trained on 4.7M examples from 7 tasks. Evaluated on 22 datasets (19 unseen), competitive with much larger models including ChatGPT and GPT-4. Fits on CPU (RoBERTa-large-sized). — [arXiv 2305.16739](https://arxiv.org/abs/2305.16739)
- MiniCheck (Tang, Laban, Durrett, EMNLP 2024): MiniCheck-FT5 has 770M parameters and is claimed to reach GPT-4-level accuracy at about 400x lower cost. Releases the LLM-AggreFact benchmark (11 datasets, ~29K test examples). Trained on 35K examples (21K ANLI plus 14K GPT-4 synthetic). MIT licence. — [arXiv 2404.10774](https://arxiv.org/abs/2404.10774), [HF model card](https://huggingface.co/lytang/MiniCheck-Flan-T5-Large)
- Reported balanced accuracy on LLM-AggreFact: MiniCheck-FT5 74.7%, GPT-4 75.3%, Claude-3 Opus 74.1%, AlignScore 70.4%. MiniCheck-Flan-T5-L is also quoted at 75.0 average. These come from a search summary, not the full table. — [search summary](https://huggingface.co/lytang/MiniCheck-Flan-T5-Large); [leaderboard](https://llm-aggrefact.github.io/)
- Model card says about 500 documents per minute on unspecified hardware and a CUDA requirement for the official package. — [HF model card](https://huggingface.co/lytang/MiniCheck-Flan-T5-Large)
- Correctness is not faithfulness (Wallat et al., SIGIR 2025 ICTIR track): distinguishes citation correctness (the cited document supports the claim) from citation faithfulness (it causally influenced generation). The search summary reports up to 57% of citations are post-rationalised. This is a secondary summary; check the paper for the exact figure. — [PDF](https://staff.fnwi.uva.nl/m.derijke/wp-content/papercite-data/pdf/wallat-2025-correctness.pdf), [search summary](https://staff.fnwi.uva.nl/m.derijke/wp-content/papercite-data/pdf/wallat-2025-correctness.pdf)
- Survey, "Attribution, Citation, and Quotation: A Survey of Evidence-based Text Generation with LLMs" (2025) — [arXiv 2508.15396](https://arxiv.org/pdf/2508.15396) (listed in search; not read)
- "Verify with Caution: The Pitfalls of Relying on Imperfect Factuality Metrics" (2025) — [arXiv 2501.14883](https://arxiv.org/pdf/2501.14883) (appeared in search; not read, flagged as a warning about verifier reliability)

### Inferences
- A CPU-feasible attribution check is: split the answer into sentences/claims, pair each with its cited passage, and score with AlignScore or a MiniCheck-RoBERTa/DeBERTa-sized model. Report the score and keep the pair in the audit log.
- Entailment alone cannot show the model used the citation. For the audit layer, state this limitation, or generate answers from the retrieved evidence only so that post-rationalisation cannot occur.

### Gaps
- No CPU latency numbers for AlignScore or MiniCheck were found in the sources I fetched. Benchmark them yourself.
- The MiniCheck full results table could not be read (PDF came back as binary). The per-dataset numbers are unconfirmed.
- I did not verify the Wallat 57% figure against the paper.

## What small models give strong verification accuracy on CPU-only hardware?

### Takeaway
Encoder-size verifiers (355M AlignScore; MiniCheck at RoBERTa/DeBERTa/Flan-T5-L scale) reach roughly GPT-4-class accuracy on LLM-AggreFact per the MiniCheck authors, and are small enough for CPU inference. Retrieval can use BM25 plus a small embedding model. Quantisation helps larger LLMs.

### Cited Findings
- DeBERTaV3 (He, Gao, Chen, ICLR 2023): GLUE 91.37 for the Large variant; a 22M-parameter extra-small variant outperforms larger baselines. Basis for many NLI verifiers. — [arXiv 2111.09543](https://arxiv.org/abs/2111.09543)
- MiniLM (Wang et al., 2020): self-attention distillation that keeps 99%+ of teacher accuracy on SQuAD 2.0 and GLUE with 50% of parameters. Basis of the all-MiniLM sentence encoders. — [arXiv 2002.10957](https://arxiv.org/abs/2002.10957)
- Sentence-BERT (Reimers & Gurevych, EMNLP 2019): reduces a 10,000-sentence similarity search from about 65 hours to about 5 seconds. — [arXiv 1908.10084](https://arxiv.org/abs/1908.10084)
- DPR (Karpukhin et al., EMNLP 2020): dense retrieval beat Lucene-BM25 by 9-19% absolute top-20 accuracy on open-domain QA. — [arXiv 2004.04906](https://arxiv.org/abs/2004.04906)
- BEIR (Thakur et al., NeurIPS 2021): BM25 is a robust zero-shot baseline. Dense and sparse retrievers often underperform out of domain. Reranking and late-interaction are better but costlier. This supports a hybrid design. — [arXiv 2104.08663](https://arxiv.org/abs/2104.08663)
- BGE / C-Pack (Xiao et al., SIGIR 2024): the bge embedding family (including bge-small variants) with multiple model sizes. Code in FlagEmbedding. The fetched summary did not list parameter counts. — [arXiv 2309.07597](https://arxiv.org/abs/2309.07597)
- LLM.int8() (Dettmers et al., NeurIPS 2022): 8-bit inference without performance degradation via vector-wise quantisation plus outlier decomposition. — [arXiv 2208.07339](https://arxiv.org/abs/2208.07339). Note it is GPU-oriented (bitsandbytes); for CPU use ONNX Runtime or llama.cpp-style GGUF, which I did not verify here.
- HerO 2 used post-training quantisation to meet computational limits and was fastest among the top three on AVeriTeC 2025. — [arXiv 2507.11004](https://arxiv.org/abs/2507.11004)
- The MiniCheck card states it outperforms same-scale specialised fact-checkers by 4-10% absolute. — [HF model card](https://huggingface.co/lytang/MiniCheck-Flan-T5-Large)

### Inferences
- Reasonable CPU stack: BM25 (rank_bm25 or Lucene) plus bge-small or all-MiniLM for hybrid retrieval, a small cross-encoder reranker, then AlignScore or MiniCheck-class verifier exported to ONNX/int8. An LLM is only called for generating the justification or for low-confidence claims. This is my design suggestion, not a tested result.
- Expect lower accuracy than LLM-based systems on multi-hop claims. AVeriTeC winners relied on gpt-4o or 70B-class open LLMs.

### Gaps
- No verified CPU throughput, ONNX export results or int8 accuracy-loss figures for MiniCheck, AlignScore or DeBERTa-NLI. These need measurement.
- Did not verify a DeBERTa NLI checkpoint's accuracy (e.g. MNLI numbers) from a model card.
- bge-small / MiniLM MTEB or BEIR scores not retrieved.
- 2025-2026 papers beyond HerO 2 and the attribution survey were thin in this pass. Items such as Bespoke-MiniCheck-7B (noted on the leaderboard summary) and newer small verifiers were not explored.
