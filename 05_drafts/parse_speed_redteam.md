### Parse Speed — Red-Team Checklist (Staged)

| Check                                                          | Status | Notes                                                                                                                                                                                   |
| -------------------------------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Provenance first-party or transparent?                         | [x]    | Boost docs; Glaze author repo; simdjson paper/docs/blog (author); nlohmann via docs/blog.                                                                                               |
| Methods complete (CPU/OS/compiler/flags/threads/version/size)? | [x]    | Present in all staged rows.                                                                                                                                                             |
| Units consistent and clearly labeled?                          | [x]    | MB/s and GB/s preserved as reported.                                                                                                                                                    |
| Parse mode specified (DOM/On-Demand/NDJSON)?                   | [x]    | Explicit in notes for each row.                                                                                                                                                         |
| Dataset comparability across libraries?                        | [ ]    | Mixed: Glaze uses 670 B custom JSON; Boost uses varied corpora; simdjson has twitter/partial_tweets/NDJSON; nlohmann similar to Boost corpora. Avoid direct comparisons without parity. |
| Hardware comparability across libraries?                       | [ ]    | No: Apple M1 vs Intel Skylake vs Sapphire Rapids. Cross-hardware comparisons require caution.                                                                                           |
| Outliers flagged and contextualized?                           | [x]    | Boost ~6000 MB/s strings-only; simdjson On-Demand ~7 GB/s; Glaze tiny-payload microbenchmarks.                                                                                          |
| Conflicting claims resolved or annotated?                      | [x]    | Mode/dataset differences explained; no direct contradictions at equal conditions in staged set.                                                                                         |
| Evidence IDs referenced in matrix/draft?                       | [x]    | All claims cite staged EVID IDs.                                                                                                                                                        |
| Gaps requiring follow-up?                                      | [ ]    | Seek first-party nlohmann/json benchmark page; add simdjson first-party DOM vs On-Demand on same hardware for tighter parity; confirm Boost results on Linux/Clang/GCC parity.          |

Next actions:

- Add parity runs (same corpus, same hardware) where possible for Boost vs simdjson vs nlohmann/json (DOM only) [curation].
- Consider normalizing to per-core throughput or reporting both absolute and per-core figures [presentation].
- Archive historical Boost strings-only benchmark URL; keep canonical 1_83_0 page as primary [hygiene].
