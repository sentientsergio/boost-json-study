# Contributing Guidelines — Boost.JSON Competitive Market Research

## 1. General Principles
- **Evidence-first**: All factual claims must originate from `02_sources/EvidenceLog.csv`.
- **Traceability**: Every matrix entry and narrative statement must link back to one or more Evidence IDs.
- **Neutrality**: Avoid subjective language; present only verifiable facts.
- **Append-only for evidence**: Never modify or delete existing EvidenceLog rows. Add a new row and mark old ones as superseded in the `notes` field if necessary.

## 2. Adding Evidence
1. Open `02_sources/EvidenceLog.csv`.
2. Append a new row with all required fields, following definitions in `02_sources/EvidenceLog.md`.
3. Ensure each row has:
   - `source_url`
   - `retrieved_date`
   - `claim` (≤ 25 words direct quote or factual paraphrase)
4. If multiple sources conflict, add both as separate rows.
5. Commit with a message like: `Add evidence: <topic> for <library>`.

## 3. Updating the Feature Matrix
1. Identify the dimension you’re updating in `03_feature_matrix/FeatureMatrix.csv`.
2. Ensure all claims for that dimension are present in the EvidenceLog with IDs.
3. Summarize the evidence for each library cell in ≤ 2 sentences.
4. Add all supporting `evidence_ids` to the `evidence_ids` column.
5. Commit with a message like: `Update matrix: <dimension>`.

## 4. Drafting Narrative Sections
1. Use `90_prompts/agent_writer.md` as the template.
2. Provide the relevant FeatureMatrix rows and their EvidenceLog entries.
3. Cite every claim inline with `[EVID:ID]`.
4. Save draft in `05_drafts/` with a clear section filename.
5. Commit with a message like: `Draft section: <section name>`.

## 5. Red-Team Review
1. Use `90_prompts/agent_redteam.md`.
2. Compare each claim in the draft to the FeatureMatrix and EvidenceLog.
3. Record results in a checklist table.
4. Flag unsupported claims for correction before merging.

## 6. Branch & PR Workflow
- **Branch naming**: `feature/<topic>` or `fix/<topic>`.
- **PRs**: Include a summary of changes and which Evidence IDs or dimensions were affected.
- **Reviews**: All changes to EvidenceLog, FeatureMatrix, or narrative require review by the lead.

## 7. Code of Conduct
- Be respectful and constructive in feedback.
- Maintain clarity in documentation.
- Focus on accuracy and completeness over speed.

---
**Status:** v0.1 — Initial guidelines.
