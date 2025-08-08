# EvidenceLog Template

```csv
evidence_id,topic,library,claim,metric,value,unit,dataset_or_code,method,source_url,source_type,author_org,pub_date,retrieved_date,notes
```

## Column definitions
- **evidence_id** — Unique identifier for each row (e.g., `EVID-0001`).
- **topic** — High-level category (e.g., "Performance: Parse Speed", "DX: API Ergonomics").
- **library** — One of `Boost.JSON`, `Glaze`, `simdjson`, `nlohmann/json`.
- **claim** — Concise factual statement supported by the source.
- **metric** — Name of the measured metric (if applicable), e.g., `parse_speed`, `memory_usage`.
- **value** — Numeric or qualitative value observed.
- **unit** — Measurement unit (e.g., `MB/s`, `ms`, `KB`, `bool`).
- **dataset_or_code** — Dataset name or code snippet reference.
- **method** — How the result was obtained (benchmark suite, profiling, doc statement, etc.).
- **source_url** — Direct link to supporting source.
- **source_type** — `documentation`, `benchmark`, `code`, `article`, etc.
- **author_org** — Author or organization responsible for the source.
- **pub_date** — Date the source was published (YYYY-MM-DD).
- **retrieved_date** — Date retrieved (YYYY-MM-DD).
- **notes** — Context, caveats, or relevant commentary.

## Notes
- Append-only: do not alter existing rows; add new rows and mark superseded claims in `notes`.
- Direct quotes ≤ 25 words.
- Each row should be specific enough to stand alone without needing the full source.
