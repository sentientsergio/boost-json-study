# Joint Post-Research Runbook — Standard Compliance (All Libraries)

This runbook is used **after all four library research runs are complete** for this dimension.  
It produces the final matrix row, the full dimension draft, and the red-team review in one set of steps.

---

## Step 0 — Prep
- Make sure `02_sources/EvidenceLog.csv` contains **all research rows** for this dimension (Boost.JSON, Glaze, simdjson, nlohmann/json).
- Confirm `03_feature_matrix/FeatureMatrix.csv` has the row for this dimension ready to update.
- Open the **Matrix Agent init block** from `90_prompts/agent_init_blocks.md`.
- Have the normalized evidence rows for this dimension ready (from `EvidenceLog.csv` or the cleaned file).

---

## Step 1 — Matrix Agent (GPT-5 standard, no Browsing)
Prompt to paste after init block:
```
[AGENT=Matrix]
dimension: Standard Compliance
evidence_subset:
<paste ALL Standard Compliance evidence rows for all libraries from EvidenceLog.csv>
Return: one CSV row:
dimension,Boost.JSON,Glaze,simdjson,nlohmann/json,notes,evidence_ids
Rules:
- Fill all four library cells.
- `notes` should capture defaults vs. opt-ins and notable deviations.
- `evidence_ids` is the union of all IDs used.
- No markdown or commentary.
```

**Save / Commit**
- Update the single `Standard Compliance` row in `03_feature_matrix/FeatureMatrix.csv` in place.
- Commit: `Matrix: complete Standard Compliance row`.

---

## Step 2 — Writer Agent (GPT-5 Thinking, no Browsing)
Prompt to paste after init block:
```
[AGENT=Writer]
section: Standard Compliance — All Libraries
feature_matrix_subset:
<paste the Standard Compliance row from FeatureMatrix.csv>
evidence_log_subset:
<paste ALL Standard Compliance evidence rows from EvidenceLog.csv>
Return: Markdown text for the full dimension section, with subsections for each library.
Rules:
- Every factual claim must cite [EVID:ID].
- Use subheadings per library for clarity.
```

**Save / Commit**
- Update or create `05_drafts/standard_compliance.md` with the new section.
- Commit: `Draft: Standard Compliance (all libraries)`.

---

## Step 3 — Red-Team Agent (GPT-5 standard, no Browsing)
Prompt to paste after init block:
```
[AGENT=Red-Team]
section_name: Standard Compliance — All Libraries
draft_text:
<paste the full Standard Compliance section from the draft file>
feature_matrix_subset:
<paste the Standard Compliance row from FeatureMatrix.csv>
evidence_log_subset:
<paste ALL Standard Compliance evidence rows from EvidenceLog.csv>
Return: Markdown checklist table with:
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
Rules:
- Mark YES if fully supported; NO otherwise.
- Do not rewrite text; only evaluate.
```

**Save / Commit**
- Append the checklist to the end of `05_drafts/standard_compliance.md` or a `_redteam.md` companion.
- Commit: `Red-Team: Standard Compliance`.

---

**End of Runbook**
