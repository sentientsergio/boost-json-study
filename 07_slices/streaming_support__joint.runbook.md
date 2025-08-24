# Joint Post-Research Runbook — Streaming Support (All Libraries)

This runbook is used after research runs for all four libraries are complete for this dimension. It produces the matrix row, the narrative section, and a red-team checklist.

---

## Step 0 — Prep

- Ensure `02_sources/EvidenceLog.csv` contains the Streaming Support evidence rows for: Boost.JSON, Glaze, simdjson, nlohmann/json.
- Confirm `03_feature_matrix/FeatureMatrix.csv` has a placeholder row for "Streaming Support" ready to update.
- Open the Matrix/Writer/Red-Team init blocks from `90_prompts/agent_init_blocks.md` and use the prompts in `90_prompts/`.

Evidence targets (collect first-party docs where possible):

- APIs for incremental/streaming parsing (push vs. pull, SAX/events, DOM builder)
- Partial/paused parse, continuation/resume, backpressure handling
- Input sources (buffers, spans, `std::istream`, file descriptors), incremental UTF-8 handling
- Output/serialization streaming (chunked emit, iterators, writer interfaces)
- Memory/allocator controls during streaming (arena, monotonic, custom allocators)
- Error reporting during streaming (recoverability, location info)
- Constraints/limits (max depth, nesting, partial tokens across chunks)
- Notes: keep performance claims out of this row unless clearly scoped in `notes`; cite them in the Performance dimensions instead.

---

## Step 1 — Matrix Agent (GPT-5 standard, no Browsing)

Prompt after init block:

```
[AGENT=Matrix]
dimension: Streaming Support
evidence_subset:
<paste ALL Streaming Support evidence rows for all libraries from EvidenceLog.csv>
Return: one CSV row:
dimension,Boost.JSON,Glaze,simdjson,nlohmann/json,notes,evidence_ids
Rules:
- Fill all four library cells with concise, factual capability summaries.
- `notes` captures important caveats (APIs, limits, opt-ins vs defaults).
- `evidence_ids` is the union of the IDs used.
- No markdown or commentary.
```

Save / Commit:

- Update the single `Streaming Support` row in `03_feature_matrix/FeatureMatrix.csv` in place.
- Commit: `Matrix: complete Streaming Support row`.

---

## Step 2 — Writer Agent (GPT-5 Thinking, no Browsing)

Prompt after init block:

```
[AGENT=Writer]
section: Streaming Support — All Libraries
feature_matrix_subset:
<paste the Streaming Support row from FeatureMatrix.csv>
evidence_log_subset:
<paste ALL Streaming Support evidence rows from EvidenceLog.csv>
Return: Markdown text for the full dimension section, with subsections per library.
Rules:
- Every factual claim must cite [EVID:ID].
- Use subheadings per library for clarity.
```

Save / Commit:

- Create or update `05_drafts/streaming_support.md` with the section.
- Commit: `Draft: Streaming Support (all libraries)`.

---

## Step 3 — Red-Team Agent (GPT-5 standard, no Browsing)

Prompt after init block:

```
[AGENT=Red-Team]
section_name: Streaming Support — All Libraries
draft_text:
<paste the full Streaming Support section from the draft file>
feature_matrix_subset:
<paste the Streaming Support row from FeatureMatrix.csv>
evidence_log_subset:
<paste ALL Streaming Support evidence rows from EvidenceLog.csv>
Return: Markdown checklist table with:
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
Rules:
- Mark YES if fully supported; NO otherwise.
- Do not rewrite text; only evaluate.
```

Save / Commit:

- Append the checklist to the end of `05_drafts/streaming_support.md` or a `_redteam.md` companion.
- Commit: `Red-Team: Streaming Support`.

---

End of Runbook
