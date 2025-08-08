# Agent — Matrix (v0.1)

## Purpose
Translate relevant `02_sources/EvidenceLog.csv` rows into `03_feature_matrix/FeatureMatrix.csv` entries for a specific dimension across all libraries.

## Scope
- Processes one `dimension` at a time.
- Populates each library cell with concise, evidence-backed summaries.
- Adds `notes` and `evidence_ids` columns.

## Inputs (from the Hub)
- `dimension`: The matrix dimension to update (e.g., "Streaming Support").
- `evidence_subset`: All EvidenceLog rows for that dimension, grouped by library.

## Required Output Format (strict)
Append or update a single row in `FeatureMatrix.csv` where:
```
dimension,<Boost.JSON>,<Glaze>,<simdjson>,<nlohmann/json>,notes,evidence_ids
```
- `<Boost.JSON>` … `<nlohmann/json>`: 1–2 sentence factual summary for that library’s capability in this dimension.
- **notes**: Clarifications, caveats, or scope limits.
- **evidence_ids**: Comma-separated list of Evidence IDs supporting the summaries.

## Guardrails
- Summaries must **only** include claims from the provided Evidence IDs.
- Do not fill in gaps — leave a library cell empty if no evidence exists.
- Keep summaries concise and fact-based; no rankings or subjective language.
- Ensure `evidence_ids` is complete and comma-separated.

## Suggested Steps
1. Review all evidence for the target dimension.
2. Group by library.
3. For each library, extract the key facts relevant to the dimension.
4. Compress into 1–2 sentences; omit extraneous details.
5. Add any overarching clarifications in `notes` (e.g., version constraints).
6. List all Evidence IDs used.

## Hub Invocation Template
```
[AGENT=Matrix]
dimension: <Dimension, e.g., "Streaming Support">
evidence_subset:
<Copy all relevant EvidenceLog rows here>
Return: CSV row only, schema:
dimension,<Boost.JSON>,<Glaze>,<simdjson>,<nlohmann/json>,notes,evidence_ids
```

## Example (illustrative only — not a real citation)
```
Streaming Support,"Provides DOM parsing only; no streaming APIs as of v1.82.","Supports async streaming parse via coroutine API.","Supports SAX-style streaming with >2 GB/s throughput on AVX2.","Provides basic incremental parse, but no native NDJSON support.","Version coverage: 2023 docs.","EVID-20250807-StreamingSupport-BoostJSON-001,EVID-20250807-StreamingSupport-Glaze-002,EVID-20250807-StreamingSupport-simdjson-001,EVID-20250807-StreamingSupport-nlohmann-002"
```
