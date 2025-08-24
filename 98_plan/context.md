# Context — Boost.JSON Competitive Market Research (v0.3 — Standard Compliance refreshed)

## Purpose of this file

This file is a working breadcrumb for current project state and next actions. It complements the root README and the Charter.

---

## Current State (as of v0.3)

- **Repository structure**: Aligned with `01_charter/Charter.md`; prompts, runbooks, and templates present.
- **Evidence**: `02_sources/EvidenceLog.csv` cleaned and normalized for the “Standard Compliance” dimension with `EVID-...` IDs; columns corrected.
- **Feature Matrix**: `03_feature_matrix/FeatureMatrix.csv` updated for “Standard Compliance” to reference new `EVID-...` IDs.
- **Drafts**:
  - `05_drafts/02_feature_matrix_narrative.md`: Updated citations to new Evidence IDs.
  - `05_drafts/02_feature_matrix_narrative redteam.md`: Checklist updated to new Evidence IDs.
  - Other chapter drafts are placeholders.
- **Benchmarks**: Plan outlined; no results logged.
- **Custom GPT Hub**: Not tracked in repo — expected to be created in OpenAI Projects and linked to this repo’s artifacts.

---

## Where We Left Off

1. Standard Compliance slice cleaned, matrix refreshed, and draft/red-team updated (G1+G2 complete for this dimension).
2. Next slice selection pending.

---

## Next Steps (short-term)

1. **Stand up Manual ChatGPT Hub (no RAG)**: Create four chats (Research, Matrix, Writer, Red‑Team), paste init blocks, set GPT‑5, and use runbooks to shuttle CSV/MD between chats and repo.
2. **Second slice**: Start “Streaming Support” research (evidence → matrix → draft → red-team).

---

## Next Steps (medium-term)

- After Streaming Support, proceed to **Performance: Parse Speed**.
- Decide benchmark scope (published-only for v1.0 vs. selective local runs).
- Begin systematic coverage of FeatureMatrix dimensions.

---

## Dependencies / Open Decisions

- Confirm C++ standard/compilers/OS constraints with client.
- Confirm whether local benchmarks are in v1.0.
- Define the sync flow from GitHub → Custom GPT Project Files (RAG refresh cadence).

---

**Status Marker**: v0.3 — Standard Compliance refreshed (G1+G2); ready to run Streaming Support slice and set up Hub.
