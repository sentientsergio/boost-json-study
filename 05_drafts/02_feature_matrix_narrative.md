# Feature Matrix Narrative

## Standard Compliance — All Libraries

### Boost.JSON

Boost.JSON states that it implements JSON as standardized in RFC 8259 and guarantees that a serialized value can be parsed back to an equivalent representation (value round-trip) [EVID:EVID-20250808-standard-compliance-boost-001][EVID:EVID-20250808-standard-compliance-boost-004].
By default, its parser accepts only strictly conforming UTF-8 JSON as determined by parse_options defaults [EVID:EVID-20250808-standard-compliance-boost-002].
Non-standard features such as comments and trailing commas are available only when explicitly enabled via parse_options flags like allow_comments and allow_trailing_commas [EVID:EVID-20250808-standard-compliance-boost-003].

### Glaze

Glaze targets modern C++ and requires C++23, leveraging concepts in its design [EVID:EVID-20250808-standard-compliance-glaze-001].
Its documentation lists testing across GCC, Clang, and MSVC on Linux, macOS, and Windows [EVID:EVID-20250808-standard-compliance-glaze-002].
The library operates via direct in-memory JSON serialization/deserialization from C++ objects [EVID:EVID-20250808-standard-compliance-glaze-003].
For input strictness, Glaze errors on unknown/extra JSON keys by default, with an opt-out that allows skipping unknown keys when configured [EVID:EVID-20250808-standard-compliance-glaze-004].

### nlohmann/json

By default the library accepts only UTF-8 input [EVID:EVID-20250808-standard-compliance-nlohmann-001].
Non-standard JSON features—comments and trailing commas—are rejected by default, but can be relaxed with explicit parse flags (ignore_comments, ignore_trailing_commas) [EVID:EVID-20250808-standard-compliance-nlohmann-002][EVID:EVID-20250808-standard-compliance-nlohmann-003][EVID:EVID-20250808-standard-compliance-nlohmann-004].
Objects are treated as unordered per the JSON model; an ordered_json alternative is available when ordered semantics are needed [EVID:EVID-20250808-standard-compliance-nlohmann-005].

### simdjson

simdjson documents full compliance with RFC 8259 [EVID:EVID-20250808-standard-compliance-simdjson-001].
It performs full UTF-8 validation and exact number parsing as part of its correctness guarantees [EVID:EVID-20250808-standard-compliance-simdjson-003].
The parser rejects NaN and Infinity as non-JSON, with such support requests tracked as non-JSON extensions [EVID:EVID-20250808-standard-compliance-simdjson-004].
A single-document size limit of 4 GiB is enforced by the library [EVID:EVID-20250808-standard-compliance-simdjson-005].
The authors also report that simdjson was the first standard-compliant JSON parser to achieve gigabytes-per-second throughput on a single core [EVID:EVID-20250808-standard-compliance-simdjson-002].

### Cross-Library Synthesis

Boost.JSON and nlohmann/json default to strict parsing and allow relaxations only via explicit options (Boost parse*options; nlohmann ignore*\* flags) [EVID:EVID-20250808-standard-compliance-boost-002][EVID:EVID-20250808-standard-compliance-boost-003][EVID:EVID-20250808-standard-compliance-nlohmann-002][EVID:EVID-20250808-standard-compliance-nlohmann-003][EVID:EVID-20250808-standard-compliance-nlohmann-004].
Glaze emphasizes schema-level strictness by erroring on unknown keys unless that behavior is disabled [EVID:EVID-20250808-standard-compliance-glaze-004].
Notable deviations/limits include simdjson’s rejection of NaN/Infinity and its 4 GiB single-document cap, while Boost allows comments and trailing commas only when flags are set [EVID:EVID-20250808-standard-compliance-simdjson-004][EVID:EVID-20250808-standard-compliance-simdjson-005][EVID:EVID-20250808-standard-compliance-boost-003].
