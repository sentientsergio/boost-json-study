### Parse Speed — Client Share (Staged for Review)

Hi there,

We completed the Parse Speed slice for Boost.JSON competitive research. Below is a quick overview, links to the exact artifacts in the repo, and a short outline of the final report we propose.

### Where to look in the repo
- Evidence (appended): `02_sources/EvidenceLog.csv` (new EVID rows for Parse Speed)
- Normalized (staged): `02_sources/intake/parse_speed__normalized__2025-08-24.csv`
- Hygiene review: `02_sources/intake/parse_speed__hygiene_report__2025-08-24.md`
- Feature Matrix row (staged): `03_feature_matrix/FeatureMatrix.csv`
- Draft narrative: `05_drafts/parse_speed.md`
- Red-Team checklist: `05_drafts/parse_speed_redteam.md`

GitHub: [Repository main branch](https://github.com/sentientsergio/boost-json-study/tree/main)

### Quick highlights (mode/dataset/hardware sensitive)
- Boost.JSON: ~567–1120 MB/s DOM on mixed/escaped corpora; 1105 MB/s on numeric-only arrays with monotonic memory [EVID:EVID-20250824-ParseSpeed-Boost-004][EVID:EVID-20250824-ParseSpeed-Boost-005][EVID:EVID-20250824-ParseSpeed-Boost-002]. Specialized strings-only case reports ~6000 MB/s (historical doc) [EVID:EVID-20250824-ParseSpeed-Boost-003].
- simdjson: ~3.0 GB/s single-core DOM (Skylake); ~6.8–7.0 GB/s On-Demand (Sapphire Rapids); NDJSON ~3.5 GB/s multi-core [EVID:EVID-20250824-ParseSpeed-simdjson-001][EVID:EVID-20250824-ParseSpeed-simdjson-002][EVID:EVID-20250824-ParseSpeed-simdjson-004][EVID:EVID-20250824-ParseSpeed-simdjson-006][EVID:EVID-20250824-ParseSpeed-simdjson-003]. DOM on the same Sapphire Rapids setup ~4.8–4.9 GB/s [EVID:EVID-20250824-ParseSpeed-simdjson-005][EVID:EVID-20250824-ParseSpeed-simdjson-007].
- nlohmann/json: Typically ~55–137 MB/s DOM on common corpora; ~0.1 GB/s reported on twitter.json under other conditions [EVID:EVID-20250824-ParseSpeed-nlohmann-002][EVID:EVID-20250824-ParseSpeed-nlohmann-003][EVID:EVID-20250824-ParseSpeed-nlohmann-004][EVID:EVID-20250824-ParseSpeed-nlohmann-005][EVID:EVID-20250824-ParseSpeed-nlohmann-006][EVID:EVID-20250824-ParseSpeed-nlohmann-001].
- Glaze: ~1.08–1.22 GB/s on a tiny 670 B custom JSON (Apple M1, single thread, in-memory struct) [EVID:EVID-20250824-ParseSpeed-Glaze-001][EVID:EVID-20250824-ParseSpeed-Glaze-002][EVID:EVID-20250824-ParseSpeed-Glaze-003][EVID:EVID-20250824-ParseSpeed-Glaze-004][EVID:EVID-20250824-ParseSpeed-Glaze-005][EVID:EVID-20250824-ParseSpeed-Glaze-006][EVID:EVID-20250824-ParseSpeed-Glaze-007].

Key caveat: Comparisons require parity on parse mode (DOM vs On-Demand/NDJSON), dataset structure, and hardware/compiler; otherwise treat as non-comparable.

### Proposed report outline (first draft)
- Executive summary: One-paragraph recap + bullets with mode/dataset caveats and the headline results per library [EVID:IDs as above].
- Methods & scope: What we counted as parse speed; how datasets, compilers, and hardware were recorded; what is out of scope.
- Results by library:
  - Boost.JSON: DOM and options (monotonic memory, reuse), dataset sensitivity, representative figures [EVID:Boost-001..005].
  - simdjson: DOM vs On-Demand vs NDJSON; per-core vs multi-core; representative figures [EVID:simdjson-001..007].
  - nlohmann/json: Typical DOM results across common corpora [EVID:nlohmann-001..006].
  - Glaze: Microbenchmarks on small JSON; interpretability and transferability [EVID:Glaze-001..007].
- Cross-library discussion: Only compare like-with-like; summarize where parity exists; open gaps for parity runs.
- Risks, gaps, and follow-ups: Items from the Red-Team checklist.
- Appendix: Evidence table (EVID rows), links to sources, and matrix snapshot.

### Next steps we recommend
- Confirm what “like-for-like” parity runs you’d want prioritized (corpus and hardware). We can queue parity experiments or limit to literature-only.
- If this scope looks good, we’ll promote staged items into the main narrative and integrate with the broader study.

Thanks — happy to walk through live or async.
