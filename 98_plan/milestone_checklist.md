# Milestone Checklist — Boost.JSON Competitive Market Research

## v0.1 — Post-Scaffold Tasks

Tracking progress after scaffolding-complete commit, leading toward first research outputs.

### Setup & Organization

- [ ] Confirm GitHub repo structure matches Charter (including numbered folders).
- [ ] Move `context.md` to `98_plan/context.md` (done if you're reading this here).
- [ ] Ensure root README.md points to correct docs and reflects current state.

### Manual ChatGPT Hub Setup (no RAG)

- [ ] Create four ChatGPT conversations: Research, Matrix, Writer, Red‑Team.
- [ ] Paste the corresponding init blocks from `90_prompts/agent_init_blocks.md` in each chat.
- [ ] Set model to GPT‑5 in each conversation.
- [ ] For each slice, follow the runbook steps to paste input context and capture outputs back into the repo.

### First Vertical Slice

- [ ] Select initial dimension for research (e.g., Standard Compliance).
- [ ] Choose one library to start with (e.g., simdjson).
- [ ] Run Research Agent to populate EvidenceLog.csv for that dimension/library.
- [ ] Review evidence entries for completeness and citation hygiene (Gate G1).

### Matrix Population

- [ ] Run Matrix Agent to update FeatureMatrix.csv for that dimension across all libraries.
- [ ] Review and freeze that dimension’s matrix row (Gate G2).

### Drafting & Review

- [ ] Run Writer Agent to produce a draft section from the matrix + evidence.
- [ ] Run Red-Team Agent to check every claim for factual grounding.
- [ ] Address any flagged issues; approve draft (Gate G3).

### Stakeholder-Ready Output

- [ ] Compile updated repo snapshot.
- [ ] Publish section to Notion for stakeholders.

---

**Note:** This checklist will expand for v1.0 to include all dimensions in FeatureMatrix, benchmark decisions, and final report assembly.
