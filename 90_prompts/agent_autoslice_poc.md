# AutoSlice POC — Parse Speed (GPT-5, Browsing Enabled)

Use this kickoff block to run a fully/mostly automated slice in one conversation. Toggle gates as needed.

## Toggles
- libraries: Boost.JSON, simdjson, nlohmann/json, Glaze
- constraints: C++20 primary; Linux/macOS/Windows; GCC/Clang/MSVC
- scope: published benches only (no local runs) — POC
- trust: proceed without human gates (G1/G2/G3) = true
- auto_commit: false (produce diffs/CSV/MD outputs only)

## Kickoff Prompt
```
[AGENT=AutoSlice]
objective: Complete the "Performance: Parse Speed" slice end-to-end.
steps:
- Research: find first-party docs and reputable/transparent benchmark sources per library; extract parse speed data and conditions.
- Hygiene: normalize to EvidenceLog schema; assign IDs EVID-<date>-ParseSpeed-<lib>-NNN; ensure source_url+retrieved_date.
- Matrix: produce one FeatureMatrix row for Parse Speed summarizing each library with evidence_ids and notes (datasets/hardware/method caveats).
- Writer: draft the section strictly from the matrix+evidence with [EVID:ID] cites only.
- Red-Team: generate the checklist table; mark conflicts/gaps clearly.
- Output: return 4 artifacts — evidence_csv, matrix_row_csv, draft_md, redteam_md.
constraints:
- Prefer first-party and peer-reviewed/transparent benches; if multiple disagree, include both and explain.
- Do not invent numbers; cite exactly as reported with dataset/hardware context in notes.
return_format:
- evidence_csv (no header)
- matrix_row_csv (single row)
- draft_md (markdown)
- redteam_md (markdown checklist table)
```

## Notes
- Keep quotes ≤ 25 words; include dataset/hardware in notes when relevant.
- If evidence is sparse, call it out; leave cells blank rather than speculate.
