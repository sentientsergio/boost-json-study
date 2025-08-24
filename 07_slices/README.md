# Slices — Manual ChatGPT Run Checklist

Use this checklist to run any dimension slice (e.g., Standard Compliance, Streaming Support) using separate ChatGPT conversations (no RAG).

## Prereqs

- Repo open to copy/paste: `02_sources/EvidenceLog.csv`, `03_feature_matrix/FeatureMatrix.csv`, `05_drafts/`, and `90_prompts/`.
- Model: GPT‑5 for all agent chats.

## 1) Prepare Chats (once per agent)

1. Create four chats named: Research, Matrix, Writer, Red‑Team.
2. Paste the corresponding init block from `90_prompts/agent_init_blocks.md` and wait for "Ready.".

## 2) Research

1. In the Research chat, paste the run command for the target dimension/library (see runbook in this folder).
2. Paste the returned CSV rows into `02_sources/EvidenceLog.csv` (append‑only, normalized IDs).

## 3) Matrix

1. In the Matrix chat, paste ALL EvidenceLog rows for this dimension.
2. Paste the returned single CSV row into `03_feature_matrix/FeatureMatrix.csv` (update the target row only).

## 4) Writer

1. In the Writer chat, paste the matrix row and the evidence rows referenced by that row.
2. Paste the returned Markdown into `05_drafts/<dimension>.md` with `[EVID:ID]` citations intact.

## 5) Red‑Team

1. In the Red‑Team chat, paste the draft, the matrix row, and the evidence rows.
2. Paste the returned checklist into the end of the draft or a `_redteam.md` companion.

## 6) Commit Hygiene

- Commit after each step with focused messages (see repo rules in `99_admin/`).

## Notes

- Do not invent facts. If evidence is missing, leave cells blank and capture gaps in `notes`.
- Prefer first‑party docs; include `method`, `source_type`, `pub_date`, and `retrieved_date`.
