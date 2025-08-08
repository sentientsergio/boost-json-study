# FeatureMatrix Template

```csv
dimension,Boost.JSON,Glaze,simdjson,nlohmann/json,notes,evidence_ids
```

Followed by one row per dimension × library.

## Column definitions
- **dimension** — The feature or capability being compared.
- **Boost.JSON … nlohmann/json** — Short text summarizing this library’s capabilities for that dimension.
- **notes** — Clarifying context, caveats, or interpretation.
- **evidence_ids** — Comma-separated list of Evidence IDs from `EvidenceLog.csv` that support this row.

## Prepopulated Dimensions
- API Design Philosophy
- Standard Compliance
- Platform Support
- Integration Ease
- Dependencies
- Licensing
- Performance: Parse Speed
- Performance: Serialize Speed
- Memory Footprint
- Streaming Support
- SIMD Utilization
- Allocator Control
- Validation Features
- Error Handling
- Documentation Quality
- Maintenance Activity

## Notes
- Fill library cells with concise, factual statements.
- Always tie claims to `EvidenceLog` rows.
- Avoid subjective language; keep evaluations evidence-based.
