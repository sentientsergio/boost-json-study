# AutoSlice Hybrid — Deep Research Gate + Automated Slice (GPT-5, Browsing Enabled)

Use this kickoff when you want a one-conversation flow that: (1) prompts the human for four deep sources first, then (2) proceeds automatically to produce all four artifacts. Defaults: published-only evidence, no human gates after paste, auto_commit=false.

## Toggles
- libraries: Boost.JSON, simdjson, nlohmann/json, Glaze (modifiable)
- dimension: e.g., Performance: Parse Speed (modifiable)
- constraints: C++20 primary; Linux/macOS/Windows; GCC/Clang/MSVC
- scope: published/transparent sources only (first-party preferred)
- human_gate: one-time paste of up to 4 sources, then automated
- auto_commit: false (produce diffs/CSV/MD outputs only)

## Kickoff Prompt
```
[AGENT=AutoSlice-Hybrid]
objective: Run a hybrid slice for "<dimension>" end-to-end with a single deep-research gate (4 pastes), then fully automate.
steps:
- Prompt the user to paste up to four sources (one per library if possible) with required fields.
- Validate the fields; if any missing, ask for just what's missing. Do not invent.
- Hygiene: normalize to EvidenceLog schema; assign IDs EVID-<date>-<dimension>-<lib>-NNN; include source_url+retrieved_date.
- Matrix: produce one FeatureMatrix row for <dimension> summarizing each library with evidence_ids and notes (datasets/hardware/method caveats).
- Writer: draft the section strictly from the matrix+evidence with [EVID:ID] cites only.
- Red-Team: generate the checklist table; mark conflicts/gaps clearly.
- Output: return 4 artifacts — evidence_csv, matrix_row_csv, draft_md, redteam_md.
constraints:
- Prefer first-party and peer-reviewed/transparent benchmarks; if multiple disagree, include both and explain.
- Do not invent numbers; cite exactly as reported with dataset/hardware context in notes.
return_format:
- evidence_csv (no header)
- matrix_row_csv (single row)
- draft_md (markdown)
- redteam_md (markdown checklist table)
```

## User Paste Template (required fields)
Paste up to four sources using this exact structure (≤25-word quotes; no smart quotes):

```
- library: <Boost.JSON|simdjson|nlohmann/json|Glaze>
  method: <benchmark|paper|documentation|blog|issue|repository>
  source_type: <first_party|maintainer|academic|third_party_transparent>
  source_url: <URL>
  pub_date: <YYYY-MM-DD or blank if unknown>
  retrieved_date: <YYYY-MM-DD>
  quote: "<=25 words direct quote or specific number"
  dataset_or_code: <dataset name or repo path>
  hardware_compiler_os: <CPU/SoC, RAM, OS, compiler/version>
  notes: <setup details, caveats, how metric is defined>
```

## Notes
- Keep quotes ≤ 25 words; include dataset/hardware in notes when relevant.
- If evidence is sparse, call it out; leave cells blank rather than speculate.

