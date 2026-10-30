# Analysis plan (frozen before results were inspected)

Frozen on 2026-10-19, after the record-flow and query-match audit (step 01) and before any
bibliometric, network, topic or annotation results were computed. The git history timestamps this file.
Changes after this point are listed under "Deviations" at the end.

## Research questions
- RQ1 Structure. How has research at the intersection of AI credibility, algorithmic bias and business
  developed (production, sources, authors, countries, impact)?
- RQ2 Themes. Which thematic clusters and latent topics organise the field, and how have they shifted?
- RQ3 Business interference map. Which business functions and which model-interference mechanisms are
  studied, and which function × mechanism combinations receive less attention than independence predicts?
- RQ4 Intellectual base. Do keyword-defined thematic clusters share intellectual foundations? We test this
  with OpenAlex-derived bibliographic coupling against permutation baselines.
- RQ5 Credibility of the pipeline. How stable are the headline findings under alternative, defensible
  analyst choices? How reliable are LLMs used as simulated expert coders, i.e. what is the simulator bias?

## Corpora
- C-full: WoS export (5,676) → article/review/proceedings paper, English, non-retracted, abstract present.
- C-core: C-full records that match all four query blocks in title/abstract/author keywords/Keywords Plus.
  The export was retrieved with the ALL= query, so C-core is the precision-oriented robustness corpus.
- Trend statistics use complete years 2018–2025. The year 2026 is partial (export 2026-05-06) and is shown separately.

## Definitions
- Simulator bias: systematic deviation between the judgements of an AI model that stands in for a human
  judge (respondent, coder, evaluator, decision maker) and the judgements of the humans it simulates. This is
  related to algorithmic fidelity (Argyle et al., 2023) and automation bias. In this study it is measured on
  LLM coders of scientific abstracts.
- Model interference: any mechanism through which properties of an AI model alter a business decision
  beyond the decision-relevant evidence. Mechanism codebook: data/sampling bias, opacity, drift/instability,
  feedback loops, over-reliance/automation bias, hallucination/fabrication, simulation/synthetic-data bias.

## Headline claims to be stress-tested (multiverse, RQ5)
H1 Annual growth rate 2018–2025 (CAGR).
H2 Rank order of the top-10 countries by documents.
H3 Membership of the five largest keyword co-occurrence clusters, measured by adjusted Rand index against the baseline.
H4 Ranking of the most and least attended function × mechanism cells (RQ3), measured by the sign of the standardized residual.
H5 Bibliographic coupling within vs. between clusters (RQ4), measured by the ratio and the permutation p.
H6 LDA topic structure, measured by best-match topic similarity across K and seeds.
Specification factors (all combinations where applicable):
  corpus {C-full, C-core}; document types {all eligible, journal articles+reviews only};
  keyword field {author keywords, Keywords Plus, both}; keyword normalisation {on, off};
  network threshold {top 100, top 200 keywords}; clustering {Louvain seeds 0..4};
  LDA K {baseline ±2} × seeds {0..4}; years {2018–2025, 2018–2026}.
Report: effect ranges and the share of specifications preserving each claim (sign/rank/ARI ≥ 0.6).
We report the distributions themselves and do not compute a composite score.

## Annotation reliability audit (RQ5)
- Sample: 400 records, stratified by publication year (proportional, with a minimum of 20 per year) and drawn with seed 2026.
  A disjoint calibration set of 40 records is used only to finalise the codebook.
- Coders: Claude (fresh isolated agent), GPT via Codex CLI (isolated non-interactive runs), and DeepSeek
  (two independent sessions, which count as within-model repeat measurements and not as independent coders).
- Input: title and abstract only (no authors, sources or years). Same prompt and codebook for every coder.
  Coders do not see any other coder's labels or the dictionary labels.
- Dimensions: relevance (corpus precision), business function (multi-label + primary), interference
  mechanism (multi-label), stance toward AI credibility (optimistic/cautious/critical/neutral-technical).
- Metrics: Krippendorff's alpha per dimension (nominal; multi-label as per-label binary alpha), with
  document-bootstrap 95% CIs; pairwise label-shift (marginal distribution differences, McNemar/Stuart-Maxwell);
  agreement of the dictionary classifier with LLM majority. A stance dimension with alpha < 0.60 is
  reported as unreliable and not used substantively.
- Human gold standard: a 60-record subsample is exported for blind double coding by two domain experts.
  Until it is coded, results are reported as inter-model agreement, not as validity.

## RQ3 statistics
Multi-label counts per record. The expected count of each function × mechanism cell under independence is
computed from the marginals. Significance comes from a permutation test that shuffles mechanism label sets
across records (10,000 permutations), with Benjamini–Hochberg FDR at q = 0.05. "Under-attended" means relative
attention and does not mean the cell is absent from the literature.

## RQ4 statistics
OpenAlex works are matched by DOI. We report the match rate and reference coverage by year and type.
Bibliographic coupling uses the Jaccard index of reference sets. We compare within-cluster and between-cluster
mean coupling, with a null that permutes cluster labels within publication year × reference-count tercile strata
(5,000 permutations).

## Deviations
1. Codebook v1.0 -> v1.1 after the planned calibration round (40 disjoint records, Claude and GPT coders):
   added decision rules for the organisational context, non-AI word senses and mechanism coding.
2. Dictionary v1.0 -> v1.1, before any annotation output was inspected: FIN matched "investigate"
   (pattern restricted to investment/investor/investing). MGT matched any "strategy" (restricted to
   business/corporate/competitive strategy and strategic management/decision/planning). LAW "regulat"
   restricted to regulation/regulatory/regulator.
3. RQ3: healthcare is reported as a separate business-only vs healthcare-only mechanism contrast and not as
   a row of the permutation map, so that the business null is not distorted by health-only records.
4. Annotation sampling settings: the coder interfaces (Claude Code, Codex CLI) do not expose temperature,
   so coders ran at interface defaults rather than at temperature 0. The within-model repeat
   (DeepSeek A vs. B) quantifies the resulting stochasticity. See annotations/RUNS.md.
5. Author-level indicators exclude 10 hyper-authored documents (> 100 authors). WoS "[sic]" placeholders for
   unrenderable characters were removed from abstracts before text analyses. The LLM coders saw the original
   abstracts, and the frozen annotation items were not regenerated.

6. Multiverse operationalisation (fixed in scripts/09_multiverse.py before the multiverse was run): a strict/broad
   mechanism-dictionary factor was added to H4. H3 is measured as the ARI over all terms shared with the
   baseline 200-keyword partition, not only the five largest clusters. H4 checks the direction of every
   baseline-significant cell. Preservation thresholds: H1 within ±10 points of baseline, H2 overlap ≥ 0.8, H6
   share of topics re-matched at cosine ≥ 0.6 of at least 0.8. For speed, H5 in the multiverse uses 200,000 sampled
   document pairs and 500 permutations, while the main test in step 07 uses all pairs and 5,000 permutations.
7. Added after internal peer review: a precision-corrected interference map (scripts/10b_core_reweighting.py).
   A TF-IDF logistic classifier, trained on the LLM-majority CORE label of the 400 audit records, predicts core
   relevance for the whole corpus, and the RQ3 map is re-estimated on the predicted-core subset.
