# Vertical Slice Runbook — Boost.JSON Research Hub

## Purpose
A repeatable step-by-step procedure for running a single comparison dimension (a "vertical slice") through the Boost.JSON Research Hub GPT Project, from evidence gathering to red-team review.

---

## Step 0 — Preparation
- **Select dimension**: e.g., "Standard Compliance".
- **Select starting library**: e.g., "Boost.JSON".
- Confirm `EvidenceLog.md` and `FeatureMatrix.md` are present in the Project's Files list.
- Decide if you will use **Standard GPT-5** (faster, focused) or **GPT-5 + DeepResearch** (broader web sweeps) for the Research step.

---

## Step 1 — Research Agent
**Model:** GPT-5 or GPT-5 + DeepResearch (as needed)

**Prompt:**
```
[AGENT=Research]
dimension: <dimension>
library: <library>
assumptions/constraints: C++20 primary; GCC/Clang/MSVC; Linux/macOS/Windows
subquestions:
- Identify explicit claims in official documentation.
- Identify any known deviations or caveats.
- Find any external validations or benchmark suites relevant to this dimension.
Return: CSV rows only, schema per EvidenceLog.csv
```

**Action:**
- Copy the CSV rows from output into `02_sources/EvidenceLog.csv`.
- Commit to GitHub if keeping a permanent record.

---

## Step 2 — Matrix Agent
**Model:** GPT-5 (standard)

**Prompt:**
```
[AGENT=Matrix]
dimension: <same dimension>
evidence_subset:
<paste the new EvidenceLog rows for this dimension/library and any other relevant libraries>
Return: one CSV row for FeatureMatrix (dimension, Boost.JSON, Glaze, simdjson, nlohmann/json, notes, evidence_ids)
```

**Action:**
- Copy the returned CSV row into `03_feature_matrix/FeatureMatrix.csv`.
- Commit to GitHub if keeping a permanent record.

---

## Step 3 — Writer Agent
**Model:** GPT-5 (standard)

**Prompt:**
```
[AGENT=Writer]
section: <section name matching the dimension>
feature_matrix_subset:
<paste the relevant FeatureMatrix row(s)>
evidence_log_subset:
<paste all referenced EvidenceLog rows>
Return: Markdown text only, with inline citations in the form [EVID:ID].
```

**Action:**
- Save the Markdown as a new file in `05_drafts/` (e.g., `standard_compliance.md`).
- Commit to GitHub if keeping a permanent record.

---

## Step 4 — Red-Team Agent
**Model:** GPT-5 (standard)

**Prompt:**
```
[AGENT=Red-Team]
section_name: <same as above>
draft_text:
<paste the draft Markdown>
feature_matrix_subset:
<paste the same FeatureMatrix row(s)>
evidence_log_subset:
<paste the same EvidenceLog rows>
Return: Markdown checklist table with columns:
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
```

**Action:**
- Review flagged claims.
- If evidence is missing or incorrect, return to Step 1 to gather more.
- Once all claims are supported, mark the section as G3-approved.

---

## Step 5 — Wrap-Up
- Push updated files to GitHub (`EvidenceLog.csv`, `FeatureMatrix.csv`, draft `.md` file).
- Optionally upload updated `.md` companions to Project Files for RAG context.
- Update `98_plan/context.md` with progress and next planned slice.
- If client-facing, prepare a short summary of findings for the selected slice.

---

**Notes:**
- Use **DeepResearch** only when a dimension/library pair is likely to have sparse or scattered evidence.
- Keep outputs clean and CSV/MD-compliant to avoid manual cleanup later.
