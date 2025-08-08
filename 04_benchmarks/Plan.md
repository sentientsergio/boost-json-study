# Benchmarks Plan (v0.1)

## Purpose
To define the scope, datasets, and methodology for optional or local benchmarks conducted during the Boost.JSON Competitive Market Research project.

## Status
- **Current approach**: Use published, reputable benchmark sources for v1.0 deliverable.
- **Optional extension**: Run targeted local benchmarks to validate or fill evidence gaps.

## Methodology (Planned)
1. **Benchmark Selection Criteria**
   - Transparency: Clear methodology, publicly available code.
   - Relevance: Tests match dimensions in FeatureMatrix (e.g., parse speed, serialize speed, memory usage).
   - Comparability: Same dataset, hardware, and build configuration across libraries.

2. **Datasets**
   - Candidate: NDJSON datasets (large and small payloads).
   - Candidate: Standard JSON test suites (e.g., JSONTestSuite).
   - Candidate: Domain-specific payloads (if relevant to client use cases).

3. **Test Environment**
   - CPU: To be specified (document model and clock speed).
   - Memory: Installed RAM size and type.
   - OS/Compiler: OS version, compiler versions, and C++ standard.
   - Build flags: Optimization levels, SIMD flags, allocator settings.

4. **Metrics Collected**
   - Parse speed (MB/s)
   - Serialize speed (MB/s)
   - Memory footprint (MB or KB)
   - Validation-only performance (MB/s)
   - Latency (ms) for small payloads
   - Streaming throughput (MB/s)

5. **Output Format**
   - All benchmark results logged as EvidenceLog entries (with `dataset_or_code` and `method` fields populated).
   - Summary tables in FeatureMatrix with `notes` indicating local vs. published origin.

## Open Decisions
- Confirm if local benchmarks will be run in v1.0 or deferred to v2.0.
- Select final datasets and hardware targets.

---
**Status:** v0.1 — Outline only, pending client decision on local benchmark scope.
