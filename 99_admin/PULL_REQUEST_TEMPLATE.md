# Pull Request Template — Boost.JSON Competitive Market Research

## Summary
<!-- Briefly describe the changes in this PR -->

## Type of Change
- [ ] New evidence entries
- [ ] Update to FeatureMatrix
- [ ] New narrative draft
- [ ] Red-Team review results
- [ ] Documentation update
- [ ] Other (please describe):

## Related Issues / Evidence IDs
<!-- List related GitHub issues or Evidence IDs touched by this PR -->

## Checklist
### Evidence
- [ ] All new evidence rows include `source_url` and `retrieved_date`.
- [ ] Claims are ≤ 25 words and fact-based.
- [ ] Conflicting sources are logged as separate rows.

### FeatureMatrix
- [ ] All claims in updated cells link to Evidence IDs in `evidence_ids` column.
- [ ] No speculative or subjective language.

### Narrative Drafts
- [ ] Every factual statement cites an Evidence ID in `[EVID:ID]` format.
- [ ] Section follows structure and scope from Charter.
- [ ] Evidence gaps are explicitly noted.

### Red-Team
- [ ] Reviewed claims match corresponding EvidenceLog entries.
- [ ] Unsupported claims flagged with notes.

### General
- [ ] Changes adhere to the Contributing Guidelines.
- [ ] Commit messages are clear and descriptive.

---
**Status:** v0.1 — Initial template.
