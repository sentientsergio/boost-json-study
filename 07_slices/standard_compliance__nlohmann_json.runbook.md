# Slice Runbook — Standard Compliance × nlohmann/json

This runbook is the **only artifact** kept under `07_slices/`. All research outputs are saved directly to the master files:
- Evidence → `02_sources/EvidenceLog.csv` (append-only)
- Matrix → `03_feature_matrix/FeatureMatrix.csv` (update the single row for the dimension)
- Draft → `05_drafts/standard_compliance.md` (update the subsection for nlohmann/json)
- Red-Team → appended to the end of `05_drafts/standard_compliance.md` (or `standard_compliance_redteam.md` if you prefer)

---

## Step 0 — Prep (once per run)
- Use **ChatGPT Project Hub** for Research (turn **GPT-5 + DeepResearch** ON).
- Use **ChatGPT Project Hub (GPT-5 standard)** for Matrix, Writer, Red-Team (no DeepResearch).
- Have the following files open in Cursor for quick edits:
  - `02_sources/EvidenceLog.csv`
  - `03_feature_matrix/FeatureMatrix.csv`
  - `05_drafts/standard_compliance.md`

---

## Step 1 — Research Agent (DeepResearch ON in Project)
**Prompt** (paste in the Project chat):
```
[AGENT=Research]
dimension: Standard Compliance
library: nlohmann/json
assumptions/constraints: C++20; GCC/Clang/MSVC; Linux/macOS/Windows
subquestions:
- Explicit standard compliance claims in official docs.
- Known deviations/caveats (opt-in vs default).
- External conformance/benchmark suites relevant to compliance.
Return: CSV rows only (no header), schema:
evidence_id,topic,library,claim,metric,value,unit,dataset_or_code,method,source_url,source_type,author_org,pub_date,retrieved_date,notes
Rules: only nlohmann/json; include source_url and retrieved_date; quotes ≤ 25 words; prefer deep section URLs; no markdown/commentary.
```

**Save / Commit**
- Append raw rows to `02_sources/EvidenceLog.csv` (no header).  
- Commit: `Evidence: Standard Compliance × nlohmann/json`

---

## Step 2 — Matrix Agent (Project, GPT-5 standard)
**Prompt** (paste in the Project chat):
```
[AGENT=Matrix]
dimension: Standard Compliance
evidence_subset:
<copy all EvidenceLog rows for this dimension and nlohmann/json>
Return: one CSV row:
dimension,Boost.JSON,Glaze,simdjson,nlohmann/json,notes,evidence_ids
Rules: fill only the nlohmann/json cell; leave others blank; cite evidence_ids used; no markdown/commentary.
```

**Save / Commit**
- Update the single row for `Standard Compliance` in `03_feature_matrix/FeatureMatrix.csv`, filling only the `nlohmann/json` cell and updating `evidence_ids` (union with any existing).  
- Commit: `Matrix: update Standard Compliance — nlohmann/json`

---

## Step 3 — Writer Agent (Project, GPT-5 standard)
**Prompt** (paste in the Project chat):
```
[AGENT=Writer]
section: Standard Compliance — nlohmann/json
feature_matrix_subset:
<paste the Standard Compliance row from FeatureMatrix>
evidence_log_subset:
<paste all Standard Compliance × nlohmann/json EvidenceLog rows>
Return: Markdown text only; every factual claim cites [EVID:ID].
```

**Save / Commit**
- Update subsection **`## nlohmann/json`** in `05_drafts/standard_compliance.md`.  
- Commit: `Draft: Standard Compliance — update nlohmann/json`

---

## Step 4 — Red-Team Agent (Project, GPT-5 standard)
**Prompt**:
```
[AGENT=Red-Team]
section_name: Standard Compliance — nlohmann/json
draft_text:
<paste the nlohmann/json subsection>
feature_matrix_subset:
<paste the Standard Compliance row>
evidence_log_subset:
<paste the Standard Compliance × nlohmann/json EvidenceLog rows>
Return: Markdown checklist:
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
```

**Save / Commit**
- Append checklist beneath the `nlohmann/json` subsection in `05_drafts/standard_compliance.md`  
  (or use `05_drafts/standard_compliance_redteam.md` if you prefer).  
- Commit: `RedTeam: Standard Compliance — nlohmann/json`

---

## Final combine for this dimension (after all four libraries)
Run **Matrix** once more to produce the complete row (all four libraries filled; notes with caveats; evidence_ids as union).  
Update `03_feature_matrix/FeatureMatrix.csv` in place.  
Optionally, run **Writer** once more to create a short comparative summary at the top of `05_drafts/standard_compliance.md`.
