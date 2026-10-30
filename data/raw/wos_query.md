# Web of Science query

Database: Web of Science Core Collection. Search date: 6 May 2026. Publication years: 2018 to 2026.

```
ALL=("artificial intelligence" OR "AI algorithm*" OR "machine learning" OR "deep learning" OR "AI model*" OR "intelligent system*")
AND ALL=("credibility" OR "trustworth*" OR "trust" OR "reliability" OR "explainab*" OR "interpretab*" OR "transparency" OR "accountability")
AND ALL=("bias" OR "fairness" OR "model bias" OR "algorithmic bias" OR "AI bias" OR "discrimination" OR "interference")
AND ALL=("business" OR "enterprise" OR "organi?ation*" OR "decision making" OR "management" OR "corporate" OR "industry" OR "commercial" OR "firm*")
```

`*` matches any ending and `?` matches one character, so `organi?ation*` retrieves both organisation and organization.

The 5,676 records were exported as full records in six files (`wos_savedrecs_part1.xls` to `wos_savedrecs_part6.xls`).
