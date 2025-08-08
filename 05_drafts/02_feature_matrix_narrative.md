# Feature Matrix Narrative

## Standard Compliance — All Libraries

### Boost.JSON

Boost.JSON states that it implements JSON as standardized in RFC 8259 and guarantees that a serialized value can be parsed back to an equivalent representation (value round-trip) [EVID:e1][EVID:e4].
By default, its parser accepts only strictly conforming UTF-8 JSON as determined by parse_options defaults [EVID:e2].
Non-standard features such as comments and trailing commas are available only when explicitly enabled via parse_options flags like allow_comments and allow_trailing_commas [EVID:e3].

### Glaze

Glaze targets modern C++ and requires C++23, leveraging concepts in its design [EVID:e5].
Its documentation lists testing across GCC, Clang, and MSVC on Linux, macOS, and Windows [EVID:e6].
The library operates via direct in-memory JSON serialization/deserialization from C++ objects [EVID:e7].
For input strictness, Glaze errors on unknown/extra JSON keys by default, with an opt-out that allows skipping unknown keys when configured [EVID:e8].

### nlohmann/json

By default the library accepts only UTF-8 input [EVID:e9].
Non-standard JSON features—comments and trailing commas—are rejected by default, but can be relaxed with explicit parse flags (ignore_comments, ignore_trailing_commas) [EVID:e10][EVID:e11][EVID:e12].
Objects are treated as unordered per the JSON model; an ordered_json alternative is available when ordered semantics are needed [EVID:e13].

### simdjson

simdjson documents full compliance with RFC 8259 [EVID:e14].
It performs full UTF-8 validation and exact number parsing as part of its correctness guarantees [EVID:e16].
The parser rejects NaN and Infinity as non-JSON, with such support requests tracked as non-JSON extensions [EVID:e17].
A single-document size limit of 4 GiB is enforced by the library [EVID:e18].
The authors also report that simdjson was the first standard-compliant JSON parser to achieve gigabytes-per-second throughput on a single core [EVID:e15].

### Cross-Library Synthesis

Boost.JSON and nlohmann/json default to strict parsing and allow relaxations only via explicit options (Boost parse*options; nlohmann ignore*\* flags) [EVID:e2][EVID:e3][EVID:e10][EVID:e11][EVID:e12].
Glaze emphasizes schema-level strictness by erroring on unknown keys unless that behavior is disabled [EVID:e8].
Notable deviations/limits include simdjson’s rejection of NaN/Infinity and its 4 GiB single-document cap, while Boost allows comments and trailing commas only when flags are set [EVID:e17][EVID:e18][EVID:e3].
