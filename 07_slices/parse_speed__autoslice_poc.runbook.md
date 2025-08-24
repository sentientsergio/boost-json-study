# AutoSlice POC Runbook — Performance: Parse Speed

This runbook describes the fully/mostly automated flow for a single slice in one conversation.

## Step 0 — Prep
- Confirm toggles in `90_prompts/agent_autoslice_poc.md`.
- Decide libraries in scope (default: all four).

## Step 1 — Kickoff (choose mode)
- Fully automated: Paste the Kickoff Prompt from `90_prompts/agent_autoslice_poc.md`.
- Hybrid deep-research: Paste the Kickoff Prompt from `90_prompts/agent_autoslice_hybrid.md`; the model will prompt for up to 4 sources, then proceed automatically.

Wait for the model to return four artifacts:
  - evidence_csv (rows in EvidenceLog schema)
  - matrix_row_csv (one row)
  - draft_md (Markdown section)
  - redteam_md (Markdown checklist)

## Step 2 — Apply outputs to repo
- Append evidence_csv to `02_sources/EvidenceLog.csv` (append-only; normalize IDs and dates if needed).
- Update/add the `Performance: Parse Speed` row in `03_feature_matrix/FeatureMatrix.csv` with the returned matrix_row_csv.
- Save draft_md to `05_drafts/parse_speed.md`.
- Save redteam_md to `05_drafts/parse_speed_redteam.md`.

## Step 3 — Commit (if auto_commit disabled)
- Evidence: `Evidence: Parse Speed — add EVID rows`
- Matrix: `Matrix: add Parse Speed row`
- Draft: `Draft: Parse Speed section`
- Red-Team: `Red-Team: Parse Speed`

## Gates
- Optional: run quick hygiene check before updating the matrix.
- Freeze the row if satisfied; otherwise, iterate once.

## Notes
- Keep published benches’ dataset/hardware/method in notes; avoid mixing apples-to-oranges.
