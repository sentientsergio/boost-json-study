# Hub Instructions — Manual ChatGPT Workflow (Boost.JSON Competitive Market Research)

## Role

You coordinate 4 separate ChatGPT conversations (Research, Matrix, Writer, Red‑Team). Each uses a specific init block and runbook. No external RAG — all context is pasted from the repo.

## Objectives

1. Align with `01_charter/Charter.md` and repo rules (Evidence‑first, Matrix‑driven writing).
2. Keep `02_sources/EvidenceLog.csv` and `03_feature_matrix/FeatureMatrix.csv` as sources of truth.
3. Ensure every narrative claim cites an Evidence ID present in the Matrix row for that section.

## Conversation Setup (once per agent)

For each agent, create a new ChatGPT conversation and set the model to GPT‑5.

- Name the chats: "Research — <dimension>/<library>", "Matrix — <dimension>", "Writer — <section>", "Red‑Team — <section>".
- Paste the corresponding init block from `90_prompts/agent_init_blocks.md` and wait for "Ready." before issuing a run command.

## Workflow (per slice)

1. Research: Paste run command + copy the relevant constraints. Paste resulting CSV rows into `02_sources/EvidenceLog.csv` (append‑only).
2. Matrix: Paste all evidence rows for the dimension. Paste the one returned CSV row into `03_feature_matrix/FeatureMatrix.csv` (update that row).
3. Writer: Paste the matrix row and the evidence rows used by that row. Paste the returned Markdown into `05_drafts/<section>.md`.
4. Red‑Team: Paste the draft, the matrix row, and the evidence rows. Paste the returned checklist into the draft or `_redteam.md`.

## Guardrails

- No new facts in narrative tasks; all narrative must cite existing Evidence IDs.
- Evidence hygiene: every Evidence row must include `source_url` and `retrieved_date`.
- Sparse data: if a matrix cell lacks evidence, leave it blank; no guessing.
- Conflicts: log all conflicting sources; explain in `notes`.

## Prompts

- `agent_init_blocks.md` — init blocks for all agents.
- `agent_research.md` — CSV‑only evidence logging.
- `agent_matrix.md` — single CSV row for the dimension.
- `agent_writer.md` — Markdown section with `[EVID:ID]` cites only.
- `agent_redteam.md` — Checklist verification.

## Tips

- When copying subsets, extract only the relevant rows from `EvidenceLog.csv` and the single target row from `FeatureMatrix.csv`.
- Maintain the CSV/MD output formats exactly; do not include commentary.

---

Status: v0.2 — Updated for manual ChatGPT hub (no RAG).
