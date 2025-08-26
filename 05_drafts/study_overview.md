### Boost.JSON Competitive Study — Overview

This overview summarizes three completed slices: Standard Compliance, Streaming Support, and Performance: Parse Speed. All statements cite Evidence IDs from the EvidenceLog; comparisons are qualified by mode/dataset/hardware constraints.

## Executive summary

- Boost.JSON: Strict RFC 8259 defaults with opt-in relaxations; strong streaming primitives; DOM parse speed in the mid hundreds of MB/s on mixed corpora, higher on numeric-only inputs [EVID:EVID-20250808-standard-compliance-boost-001][EVID:EVID-20250808-standard-compliance-boost-002][EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-ParseSpeed-Boost-004][EVID:EVID-20250824-ParseSpeed-Boost-002].
- simdjson: Full RFC compliance with UTF-8 validation; NDJSON and On-Demand modes; state-of-the-art throughput in both DOM and On-Demand parsing [EVID:EVID-20250808-standard-compliance-simdjson-001][EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-simdjson-002][EVID:EVID-20250824-ParseSpeed-simdjson-001][EVID:EVID-20250824-ParseSpeed-simdjson-004].
- nlohmann/json: Strict by default with opt-in relaxations; SAX available; typical DOM throughput in tens to low hundreds of MB/s on common corpora [EVID:EVID-20250808-standard-compliance-nlohmann-001][EVID:EVID-20250824-StreamingSupport-nlohmann-001][EVID:EVID-20250824-ParseSpeed-nlohmann-002].
- Glaze: C++23-oriented, in-memory (de)serialization; no incremental parser; author-reported microbenchmarks ~1.08–1.22 GB/s on tiny payloads (Apple M1) [EVID:EVID-20250808-standard-compliance-glaze-001][EVID:EVID-20250824-StreamingSupport-Glaze-001][EVID:EVID-20250824-ParseSpeed-Glaze-006].

Key caveat: Compare like-with-like only (parse mode, dataset structure, hardware/compiler). Cross-mode or cross-hardware results are non-comparable without normalization.

## Feature Matrix snapshot (high-level)

- Standard Compliance: All libraries target RFC 8259; Boost and nlohmann provide opt-in relaxations; simdjson documents explicit limits (e.g., >4 GiB) [EVID:EVID-20250808-standard-compliance-boost-003][EVID:EVID-20250808-standard-compliance-nlohmann-004][EVID:EVID-20250808-standard-compliance-simdjson-005].
- Streaming Support: Boost supports SAX and incremental DOM; simdjson supports NDJSON and On-Demand; nlohmann has SAX but no resume/NDJSON; Glaze lacks incremental parse but has `partial_read` [EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-nlohmann-003][EVID:EVID-20250824-StreamingSupport-Glaze-004].
- Parse Speed: Representative, mode-matched summaries are included below with EVID citations.

## Slice details

### Standard Compliance

- Boost.JSON: Implements RFC 8259; defaults strict UTF-8; relaxations (comments/trailing commas) are opt-in via `parse_options` [EVID:EVID-20250808-standard-compliance-boost-001][EVID:EVID-20250808-standard-compliance-boost-002][EVID:EVID-20250808-standard-compliance-boost-003].
- simdjson: Claims full RFC 8259 compliance; full UTF-8 validation; known 4 GiB document limit [EVID:EVID-20250808-standard-compliance-simdjson-001][EVID:EVID-20250808-standard-compliance-simdjson-003][EVID:EVID-20250808-standard-compliance-simdjson-005].
- nlohmann/json: Strict defaults (UTF-8 only; no comments/trailing commas). Flags allow ignoring comments/trailing commas [EVID:EVID-20250808-standard-compliance-nlohmann-001][EVID:EVID-20250808-standard-compliance-nlohmann-002][EVID:EVID-20250808-standard-compliance-nlohmann-003][EVID:EVID-20250808-standard-compliance-nlohmann-004].
- Glaze: Modern C++ focus; documentation indicates strict behavior on unknown keys by default (opt-out) [EVID:EVID-20250808-standard-compliance-glaze-001][EVID:EVID-20250808-standard-compliance-glaze-004].

### Streaming Support

- Boost.JSON: Incremental SAX via `basic_parser`; incremental DOM via `stream_parser`; chunked input; partial token callbacks; streaming serializer [EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-StreamingSupport-BoostJSON-002][EVID:EVID-20250824-StreamingSupport-BoostJSON-003][EVID:EVID-20250824-StreamingSupport-BoostJSON-008][EVID:EVID-20250824-StreamingSupport-BoostJSON-006].
- simdjson: NDJSON (`parse_many`/`iterate_many`); On-Demand for lazy, high-throughput reads without full DOM [EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-simdjson-002].
- nlohmann/json: SAX available; no resume/incremental parse; JSON Lines not directly supported; no streaming serializer [EVID:EVID-20250824-StreamingSupport-nlohmann-001][EVID:EVID-20250824-StreamingSupport-nlohmann-002][EVID:EVID-20250824-StreamingSupport-nlohmann-003][EVID:EVID-20250824-StreamingSupport-nlohmann-005].
- Glaze: No incremental/chunked parse (contiguous buffer expected); `partial_read` supports compile-time partial parsing [EVID:EVID-20250824-StreamingSupport-Glaze-001][EVID:EVID-20250824-StreamingSupport-Glaze-004].

### Performance: Parse Speed

- Boost.JSON (DOM): ~567–1120 MB/s on mixed/escaped corpora; 1105 MB/s on a numeric-only array with a monotonic memory resource; specialized strings-only case ~6000 MB/s (historical) [EVID:EVID-20250824-ParseSpeed-Boost-005][EVID:EVID-20250824-ParseSpeed-Boost-004][EVID:EVID-20250824-ParseSpeed-Boost-002][EVID:EVID-20250824-ParseSpeed-Boost-003].
- simdjson: ~3.0 GB/s single-core DOM (Skylake-era); ~6.8–7.0 GB/s On-Demand (Sapphire Rapids); NDJSON document streams ~3.5 GB/s (multi-core) [EVID:EVID-20250824-ParseSpeed-simdjson-001][EVID:EVID-20250824-ParseSpeed-simdjson-002][EVID:EVID-20250824-ParseSpeed-simdjson-004][EVID:EVID-20250824-ParseSpeed-simdjson-006][EVID:EVID-20250824-ParseSpeed-simdjson-003].
- nlohmann/json (DOM): ~55–137 MB/s across canada/random/twitter; ~0.1 GB/s reported for twitter.json under different platform conditions [EVID:EVID-20250824-ParseSpeed-nlohmann-002][EVID:EVID-20250824-ParseSpeed-nlohmann-003][EVID:EVID-20250824-ParseSpeed-nlohmann-004][EVID:EVID-20250824-ParseSpeed-nlohmann-005][EVID:EVID-20250824-ParseSpeed-nlohmann-006][EVID:EVID-20250824-ParseSpeed-nlohmann-001].
- Glaze: ~1.08–1.22 GB/s on 670 B custom JSON (Apple M1, single thread, in-memory struct); interpret as microbenchmark [EVID:EVID-20250824-ParseSpeed-Glaze-001][EVID:EVID-20250824-ParseSpeed-Glaze-002][EVID:EVID-20250824-ParseSpeed-Glaze-006].

## Cross-library considerations

- Like-for-like comparisons require parity in mode (DOM vs On-Demand/NDJSON), dataset content/size, hardware/compiler flags, and threading. Otherwise, treat results as non-comparable [EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-ParseSpeed-simdjson-004].

## Red-Team summary (risks & gaps)

- Dataset/hardware parity gaps persist (e.g., tiny payloads on M1 vs large corpora on x86). Plan parity runs or scope guardrails before cross-library claims.
- Historical/ephemeral links (e.g., specialized strings-only case) should be archived and secondary to canonical docs [EVID:EVID-20250824-ParseSpeed-Boost-003].
- Confirm first-party nlohmann/json performance page (if any) to complement third-party measurements.

## Appendix pointers

- EvidenceLog: `02_sources/EvidenceLog.csv` (all EVID rows)
- Feature Matrix: `03_feature_matrix/FeatureMatrix.csv`
- Slice drafts: `05_drafts/streaming_support.md`, `05_drafts/parse_speed.md`
- Red-Team: `05_drafts/parse_speed_redteam.md`
