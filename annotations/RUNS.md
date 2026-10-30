# Annotation runs (provenance)

All coders received CODEBOOK.md (v1.1) and PROMPT.md verbatim, title and abstract only, in a coder-specific
random order (items_<coder>.jsonl), with no access to other coders' outputs or to the dictionary classifier.
Coding took place on 2026-10-19.

| Coder | Model | Interface | Isolation | Sampling |
|---|---|---|---|---|
| claude | Claude Opus 5.5 (`claude-opus-5-5`) | Claude Code 2.1.303 subagents, 4 batches of 100 (chunks/items_claude_part*.jsonl) | fresh context per batch | interface defaults (not exposed) |
| gpt | `gpt-6.1-sol`, reasoning effort high | OpenAI Codex CLI 0.163.0 (`codex exec`, workspace-write sandbox), 4 batches of 100 | fresh non-interactive run per batch | interface defaults (not exposed) |
| deepseek_a | `deepseek-flash` (1M context) | Claude Code 2.1.303 session A | separate session, instructed not to read other files | interface defaults (not exposed) |
| deepseek_b | `deepseek-flash` (1M context) | Claude Code 2.1.303 session B | separate session, instructed not to read other files | interface defaults (not exposed) |

Calibration (40 disjoint records, calibration/): Claude and GPT only, before the codebook was frozen.

The two DeepSeek sessions had taken part in the design discussion, so they knew the study's aims. They had
not seen the dictionary or any other coder's labels. DeepSeek A vs. B is a within-model repeat measurement,
not an independent coder.

Raw outputs: raw/*.jsonl. Validated long format: labels_long.csv.
Human gold standard: human_gold_sheet.csv (60 records, columns for two blind human coders), not yet coded.
