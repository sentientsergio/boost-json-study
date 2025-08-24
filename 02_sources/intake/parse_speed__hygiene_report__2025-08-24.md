## Parse Speed — Evidence Hygiene (2025-08-24)

Scope: Boost.JSON, simdjson, nlohmann/json, Glaze. Review of staged intake files for transparency/completeness prior to EvidenceLog append.

- Provenance

  - Boost.JSON: First-party docs (benchmarks page) + one historical pre-release doc URL. OK, note ephemeral link for strings.json.
  - simdjson: Mix of first-party (paper/docs) and Daniel Lemire blog posts (first-party author; methods detailed). Mark as blog in source_type.
  - nlohmann/json: Mix of third-party blog and Boost docs citing measured results. Prefer first-party if available; acceptable with method transparency flagged.
  - Glaze: First-party GitHub README in author’s repo. OK.

- Method completeness (CPU/OS/compiler/flags/threads/library version/dataset size)

  - Present for all rows; includes CPU family, OS, compiler and flags, threading, library version/commit, dataset description/size. OK.

- Metrics/units

  - Throughput values preserved as reported (MB/s or GB/s). OK.

- Parse mode

  - Labeled in notes (DOM, On-Demand, NDJSON parse_many, in-memory struct). OK.

- Caveats/limits

  - Glaze results are microbenchmarks on very small JSON (670 B) on Apple M1; note limited external validity.
  - Boost strings.json is a specialized case (unescaped long strings) with historical doc URL; note context.
  - simdjson multi-GB/s figures include On-Demand mode and modern CPUs; not directly comparable to DOM-only libraries; ensure comparisons respect modes and hardware.
  - nlohmann/json results largely from comparative pages/blogs; treat as indicative; seek first-party corroboration if available.

- Formatting hygiene

  - Smart quotes/Unicode normalized in normalized CSV; raw intake preserved verbatim.
  - Quotes in claims are paraphrases (not direct quotes); ≤25-word rule for direct quotes not triggered.

- Actions before append (G1 gate)
  - Keep all rows; mark provenance as first-party/blog explicitly (done).
  - Add note on Glaze microbenchmark size and parse mode in notes (present).
  - Flag Boost historical URL as archival and retain primary 1_83_0 page references.

No blockers identified for EvidenceLog append. Proceed to matrix staging, then draft and red-team using these EVID IDs.
