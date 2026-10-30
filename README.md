# Credibility of AI algorithms and model interference in business: bibliometric study data

Data for the study "Credibility of AI algorithms and model interference in business: A citation-enriched bibliometric analysis with a multiverse and multi-LLM audit" by A.-G. Văduva, C. Iancu, S.-V. Oprea and A. Bâra (Bucharest University of Economic Studies).

## Contents

| Folder | Content |
|---|---|
| `data/raw/` | Web of Science export (5,676 records in six files) and the search query |
| `data/external/` | OpenAlex snapshot: matched works and their referenced works (gzip JSONL) |
| `data/processed/` | Analysis corpus and document-level outputs |
| `annotations/` | Codebook, prompt, coder inputs and outputs of the multi-LLM annotation audit |
| `docs/` | Frozen analysis plan with its documented deviations |
| `results/tables/` | Result tables (CSV) behind the figures and tables of the article |

## Processed files

| File | Content |
|---|---|
| `corpus_all.parquet` | All 5,676 exported records after parsing |
| `corpus.parquet` | Analysis corpus (5,536 records) with derived fields such as countries and query-block matches |
| `doc_themes.csv` | Keyword theme assigned to each document |
| `doc_topics.parquet` | LDA topic proportions per document (14 topics) |
| `doc_dictionary_labels.parquet` | Business functions and interference mechanisms assigned by the dictionary classifier |

Records are identified by their WoS accession number (`UT`), and the field names follow the WoS export tags (for example `TI` title, `AB` abstract, `DE` author keywords, `PY` publication year).

## Code

The analysis code is available from the corresponding author upon reasonable request.

## License

The data produced by the authors (processed files, annotations, result tables and documentation) are released under CC BY 4.0. The raw Web of Science records remain subject to the Clarivate terms of use, and the OpenAlex data are released by OpenAlex under CC0.

## Contact

Alin-Gabriel Văduva, alin.vaduva@csie.ase.ro
