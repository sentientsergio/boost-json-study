## Boost.JSON Competitive Study — Combined Narrative Draft (Staged)

### Executive summary

- Boost.JSON defaults to strict RFC 8259 compliance with opt-in relaxations; it offers solid streaming primitives and mid-hundreds MB/s DOM parse speeds on mixed corpora, higher on numeric-heavy inputs [EVID:EVID-20250808-standard-compliance-boost-001][EVID:EVID-20250808-standard-compliance-boost-002][EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-ParseSpeed-Boost-004][EVID:EVID-20250824-ParseSpeed-Boost-002].
- simdjson delivers full RFC compliance, NDJSON and On-Demand modes, and state-of-the-art throughput in both DOM and On-Demand parsing [EVID:EVID-20250808-standard-compliance-simdjson-001][EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-simdjson-002][EVID:EVID-20250824-ParseSpeed-simdjson-001][EVID:EVID-20250824-ParseSpeed-simdjson-004].
- nlohmann/json is strict by default with SAX support; typical DOM throughput is in the tens to low hundreds of MB/s on common corpora [EVID:EVID-20250808-standard-compliance-nlohmann-001][EVID:EVID-20250824-StreamingSupport-nlohmann-001][EVID:EVID-20250824-ParseSpeed-nlohmann-002].
- Glaze emphasizes modern C++ and in-memory (de)serialization; it lacks incremental parsing but reports ~1.08–1.22 GB/s on tiny custom JSON microbenchmarks (Apple M1) [EVID:EVID-20250808-standard-compliance-glaze-001][EVID:EVID-20250824-StreamingSupport-Glaze-001][EVID:EVID-20250824-ParseSpeed-Glaze-006].

Note on comparability: Compare like-with-like only (mode, dataset, hardware/compiler); avoid cross-mode or cross-hardware conclusions without normalization.

### Standard Compliance

- Boost.JSON implements JSON per RFC 8259 and defaults to strict UTF-8; comments and trailing commas are available only via explicit `parse_options` [EVID:EVID-20250808-standard-compliance-boost-001][EVID:EVID-20250808-standard-compliance-boost-002][EVID:EVID-20250808-standard-compliance-boost-003].
- simdjson claims full RFC 8259 compliance with full UTF-8 validation and notes a single-document size limit (≈4 GiB) [EVID:EVID-20250808-standard-compliance-simdjson-001][EVID:EVID-20250808-standard-compliance-simdjson-003][EVID:EVID-20250808-standard-compliance-simdjson-005].
- nlohmann/json defaults to strict JSON (UTF-8 only; comments/trailing commas rejected) with flags to ignore non-standard inputs when desired [EVID:EVID-20250808-standard-compliance-nlohmann-001][EVID:EVID-20250808-standard-compliance-nlohmann-002][EVID:EVID-20250808-standard-compliance-nlohmann-003][EVID:EVID-20250808-standard-compliance-nlohmann-004].
- Glaze requires newer C++; unknown keys error by default (configurable) [EVID:EVID-20250808-standard-compliance-glaze-001][EVID:EVID-20250808-standard-compliance-glaze-004].

### Streaming Support

- Boost.JSON provides incremental SAX via `basic_parser`, incremental DOM via `stream_parser`, chunked input handling, partial token callbacks, and a streaming serializer [EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-StreamingSupport-BoostJSON-002][EVID:EVID-20250824-StreamingSupport-BoostJSON-003][EVID:EVID-20250824-StreamingSupport-BoostJSON-008][EVID:EVID-20250824-StreamingSupport-BoostJSON-006].
- simdjson supports NDJSON via `parse_many`/`iterate_many` and an On-Demand API for lazy parsing without building a full DOM [EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-simdjson-002].
- nlohmann/json offers SAX but no incremental/resume parsing; JSON Lines/NDJSON not directly supported; no streaming serializer [EVID:EVID-20250824-StreamingSupport-nlohmann-001][EVID:EVID-20250824-StreamingSupport-nlohmann-002][EVID:EVID-20250824-StreamingSupport-nlohmann-003][EVID:EVID-20250824-StreamingSupport-nlohmann-005].
- Glaze expects contiguous input and does not offer incremental parsing; `partial_read` enables compile-time field selection [EVID:EVID-20250824-StreamingSupport-Glaze-001][EVID:EVID-20250824-StreamingSupport-Glaze-004].

### Performance: Parse Speed

- Boost.JSON (DOM): ~567–1120 MB/s on mixed/escaped corpora; ~1105 MB/s on a numeric-only array with a monotonic memory resource; specialized strings-only case ~6000 MB/s (historical) [EVID:EVID-20250824-ParseSpeed-Boost-005][EVID:EVID-20250824-ParseSpeed-Boost-004][EVID:EVID-20250824-ParseSpeed-Boost-002][EVID:EVID-20250824-ParseSpeed-Boost-003].
- simdjson: ~3.0 GB/s single-core DOM on Skylake-era CPUs; ~6.8–7.0 GB/s On-Demand on Sapphire Rapids; NDJSON document streams ~3.5 GB/s (multi-core) [EVID:EVID-20250824-ParseSpeed-simdjson-001][EVID:EVID-20250824-ParseSpeed-simdjson-002][EVID:EVID-20250824-ParseSpeed-simdjson-004][EVID:EVID-20250824-ParseSpeed-simdjson-006][EVID:EVID-20250824-ParseSpeed-simdjson-003].
- nlohmann/json (DOM): ~55–137 MB/s across common corpora; ~0.1 GB/s reported for twitter.json under different platform conditions [EVID:EVID-20250824-ParseSpeed-nlohmann-002][EVID:EVID-20250824-ParseSpeed-nlohmann-003][EVID:EVID-20250824-ParseSpeed-nlohmann-004][EVID:EVID-20250824-ParseSpeed-nlohmann-005][EVID:EVID-20250824-ParseSpeed-nlohmann-006][EVID:EVID-20250824-ParseSpeed-nlohmann-001].
- Glaze: ~1.08–1.22 GB/s on a 670 B custom JSON (Apple M1, single thread, in-memory struct); interpret as microbenchmark [EVID:EVID-20250824-ParseSpeed-Glaze-001][EVID:EVID-20250824-ParseSpeed-Glaze-002][EVID:EVID-20250824-ParseSpeed-Glaze-006].

### Risks & caveats

- Cross-library comparisons must match mode (DOM vs On-Demand/NDJSON), dataset structure/size, hardware, compiler/flags, and threading; otherwise treat as non-comparable [EVID:EVID-20250824-StreamingSupport-simdjson-001][EVID:EVID-20250824-StreamingSupport-BoostJSON-001][EVID:EVID-20250824-ParseSpeed-simdjson-004].
- Historical/ephemeral links (e.g., specialized strings-only case) should be archived and secondary to canonical docs [EVID:EVID-20250824-ParseSpeed-Boost-003].
- Seek first-party nlohmann/json performance references (if any) to complement third-party measurements.

### Next steps (writing phase)

- Expand this draft into the full study narrative, preserving [EVID:ID] cites and scope guardrails.
- Integrate the Feature Matrix snapshot and Red-Team notes inline.
- The repository is the deliverable; no PDF production is planned. Consolidate narrative and matrices here with clear [EVID:ID] cites.
