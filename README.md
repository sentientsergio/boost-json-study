# Boost.JSON Competitive Market Research

## Overview
This repository contains all artifacts for the Boost.JSON Competitive Market Research project. The goal is to produce a 10–15 page analysis comparing Boost.JSON against three other widely used C++ JSON libraries:

- Glaze
- simdjson
- JSON for Modern C++ (nlohmann/json)

## Structure
```
01_charter/           Project charter and scope documents.
02_sources/           Evidence log (CSV + MD).
03_feature_matrix/    Feature matrix (CSV + MD).
04_benchmarks/        Benchmark plans and results.
05_drafts/            Draft report sections.
90_prompts/           Agent prompt templates.
99_admin/             Repo metadata and contributor guidelines.
```

## Workflow Summary
1. **Evidence-first** — All claims originate from `02_sources/EvidenceLog.csv`.
2. **Matrix-driven writing** — Narrative content is generated from `03_feature_matrix/FeatureMatrix.csv`.
3. **Red-team review** — Drafts are checked for factual grounding before approval.
4. **Versioning** — GitHub used as the single source of truth; Notion hosts stakeholder snapshots.

## How to Use
- To contribute evidence: append new rows to `EvidenceLog.csv` following `EvidenceLog.md` rules.
- To update the matrix: only after evidence has been reviewed and approved.
- To generate narrative sections: use `agent_writer.md` prompt template with the relevant matrix and evidence subsets.
- To review: use `agent_redteam.md` to fact-check drafts.

## Licensing
The repository content is proprietary to the commissioning client unless otherwise agreed.
