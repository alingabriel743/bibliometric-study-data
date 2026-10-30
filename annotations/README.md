# Annotations

Multi-LLM annotation audit of 400 abstracts from the analysis corpus.

| File | Content |
|---|---|
| CODEBOOK.md | Frozen codebook v1.1 (relevance, business functions, interference mechanisms, stance) |
| PROMPT.md | Instruction given verbatim to every coder |
| RUNS.md | Models, interfaces, batches, isolation and sampling |
| calibration_items.jsonl, calibration/ | 40 calibration records and the Claude and GPT calibration codes |
| audit_items.jsonl, audit_sample_key.csv | 400 audit records (stratified by year, seed 2026), their WoS IDs and design weights |
| items_*.jsonl, chunks/ | Coder-specific random orders and the 100-record batches for Claude and GPT |
| raw/ | Raw coder outputs, one JSON object per record |
| labels_long.csv | Validated labels in long format, one row per coder and record |
| human_gold_sheet.csv | 60 audit records prepared for blind double coding by two human experts |

The human columns of `human_gold_sheet.csv` (H1_*, H2_*) are not yet coded. Until they are, the audit measures agreement between models (reliability) and not validity.
