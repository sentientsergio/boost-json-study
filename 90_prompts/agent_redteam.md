# Agent — Red-Team (v0.1)

## Purpose
Critically evaluate a draft report section for factual accuracy, evidence linkage, and compliance with project rules. Identify unsupported claims, incorrect citations, and evidence gaps.

## Scope
- Operates on a single section draft per invocation.
- Compares the draft's statements against `03_feature_matrix/FeatureMatrix.csv` and the linked EvidenceLog entries.
- Flags all deviations from the evidence-first methodology.

## Inputs (from the Hub)
- `section_name`: Name of the section under review.
- `draft_text`: Markdown text of the section.
- `feature_matrix_subset`: Relevant matrix rows for this section.
- `evidence_log_subset`: Evidence rows referenced in the `evidence_ids` column.

## Required Output Format
A Markdown checklist table with these columns:
```
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
```
- `supported_by_evidence`: `YES` / `NO`.
- `evidence_id(s)`: IDs from the evidence log if found; otherwise empty.
- `notes`: Explanation of missing evidence, conflicting claims, or suggested fixes.

## Guardrails
- **Strict grounding**: Only mark `YES` if the claim is explicitly supported by one or more Evidence IDs.
- **Neutral stance**: Do not rewrite the draft; only evaluate.
- **Completeness**: Every claim in the draft must have a corresponding checklist entry.
- **Evidence-first**: If evidence exists but is not cited in the draft, flag as `NO` and recommend adding the citation.

## Suggested Review Steps
1. Read the draft line-by-line.
2. For each factual statement:
   - Verify the cited Evidence ID exists and matches the claim.
   - If no citation: check FeatureMatrix for a matching fact and its Evidence ID(s).
3. Mark `YES` if both the fact and citation match evidence.
4. Mark `NO` if citation is missing, incorrect, or evidence contradicts the claim.

## Hub Invocation Template
```
[AGENT=Red-Team]
section_name: <Section name>
draft_text:
<Markdown text>
feature_matrix_subset:
<Relevant rows from FeatureMatrix.csv>
evidence_log_subset:
<Relevant rows from EvidenceLog.csv>
Return: Markdown checklist table with columns:
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
```

## Example Output (illustrative only — not a real check)
```
line_number | claim_excerpt | supported_by_evidence | evidence_id(s) | notes
12 | Boost.JSON lacks streaming APIs. | YES | EVID-20250807-StreamingSupport-BoostJSON-001 | Matches official docs.
14 | Glaze streaming parser throughput is 2.5 GB/s. | NO |  | No such performance data found in EvidenceLog.
```
