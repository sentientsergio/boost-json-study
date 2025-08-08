# Boost.JSON Competitive Market Research — Project Charter (v0.1, updated)

## 1) Overview
We will produce a rigorous, citable, and decision-ready comparison of **Boost.JSON** against three widely used C++ JSON libraries. The outcome is a 10–15 page analysis plus supporting artifacts (feature matrix, evidence log, and curated benchmark synthesis) suitable for technical audiences and decision-makers.

## 2) Libraries in Scope (D0.1 — locked)
- **Boost.JSON** (focus of the study)
- **Glaze**
- **simdjson**
- **JSON for Modern C++** (aka *nlohmann/json*)

> If the client requests alternates (e.g., RapidJSON), we can swap one comparator without disturbing the workflow.

## 3) Goals & Deliverables
**Core report (10–15 pages)**
- **Executive Summary** (clear “winner by use case” + rationale)
- **Feature Matrix Narrative** (explain key differences)
- **Performance Analysis** (published benches synthesis; v2 may add our microbenches)
- **Developer Experience (DX)** (API ergonomics, docs, examples, maintenance cadence)
- **Integration & Ops Considerations** (deps, licensing, portability, error handling)

**Supporting artifacts**
- `03_feature_matrix/FeatureMatrix.csv` — Canonical matrix (paired with `FeatureMatrix.md` for column definitions)
- `02_sources/EvidenceLog.csv` — Append-only evidence table (paired with `EvidenceLog.md` for column definitions)
- `04_benchmarks/Plan.md` — Scope for any optional/local benches
- Prompt library for agents (Hub + Research + Matrix + Writer + Red-Team)

## 4) Constraints & Assumptions (TBD → operating assumptions for now)
- **C++ standard:** assume C++20 primary; note C++17 compatibility where relevant.
- **Compilers/OS:** GCC 12+/Clang 14+/MSVC 2022 on Linux/macOS/Windows.
- **Data shapes:** small/medium/large DOM, streaming, validation-only.
- **I/O:** UTF-8 default; call out non-UTF use cases explicitly.
- **Build system:** CMake; package managers (vcpkg/conan) noted when relevant.
> These are *assumptions* until client confirms. We will annotate findings if constraints later differ.

## 5) Winner Rubric (evidence-first)
We **do not force** a single numeric score. We:
- Report metrics as found (including gaps/sparse data).
- Map each **use case** to a clear recommendation with **evidence IDs**.
- Examples of use cases:
  - **High-throughput parsing** (large payloads, streaming)
  - **Low-latency request/response**
  - **Memory-constrained environments**
  - **DX-first development** (ergonomics/maintainability)
  - **Strict standards/validation**

## 6) Evidence & Citation Rules
- Every claim must reference at least one **Evidence ID** (row in `EvidenceLog.csv`).
- Acceptable sources: official docs, reputable repos, academic/industry posts, benchmark suites with transparent methodology.
- Direct quotes ≤ 25 words each. Always include URL and retrieval date.
- Conflicting sources are recorded side-by-side; we explain divergences.

**EvidenceLog.csv columns (canonical)**
`evidence_id, topic, library, claim, metric, value, unit, dataset_or_code, method, source_url, source_type, author_org, pub_date, retrieved_date, notes`

## 7) Roles & Workflow

### Roles (human + agents)
- **Sponsor/Client:** sets priorities, approves scope changes.
- **Editor/Lead (you):** final sign-off; owns stakeholder comms and Notion snapshots.
- **Research Agent (“Deep Research”):** breadth-first sweeps; populates EvidenceLog.
- **GPT-5 Research (me):** targeted, precision retrieval; reconciliation and synthesis.
- **Matrix Agent:** translates EvidenceLog into FeatureMatrix entries (with notes).
- **Writer Agent:** drafts chapters strictly from FeatureMatrix + Evidence IDs.
- **Red-Team Agent:** challenges unsupported assertions; flags missing evidence.

### Gates
1. **G1 — Evidence Hygiene:** Each new batch of evidence rows gets a quick review.
2. **G2 — Matrix Freeze (per dimension):** When evidence is sufficient/consistent.
3. **G3 — Draft Review:** Writer → Red-Team → Lead approval.
4. **G4 — Executive Summary:** Last; based on frozen sections only.

## 8) Artifacts & Repository Structure (SoT = GitHub; Notion = snapshots)
```
boost-json-study/
  01_charter/Charter.md
  02_sources/
    EvidenceLog.csv
    EvidenceLog.md
  03_feature_matrix/
    FeatureMatrix.csv
    FeatureMatrix.md
  04_benchmarks/
    Plan.md
  05_drafts/
    01_executive_summary.md
    02_feature_matrix_narrative.md
    03_performance.md
    04_developer_experience.md
    05_integration.md
  90_prompts/
    hub_instructions.md
    agent_research.md
    agent_matrix.md
    agent_writer.md
    agent_redteam.md
  99_admin/
    CONTRIBUTING.md
    PULL_REQUEST_TEMPLATE.md
    README.md
```

## 9) Definition of Done (DoD)
- **EvidenceLog** (CSV + MD) is complete and internally consistent (no orphan claims).
- **FeatureMatrix** (CSV + MD) rows cite Evidence IDs and reflect final constraints.
- **All chapters** drafted, red-teamed, and approved (G3).
- **Executive Summary** ties recommendations to specific use cases + evidence.
- **Repo tagged v1.0**; Notion snapshot exported for stakeholders.

## 10) Risks & Mitigations
- **Sparse/contradictory benchmarks:** Log conflicts explicitly; prefer multi-source convergence; mark “evidence gap” where needed.
- **Scope churn on constraints:** Keep assumptions section live; rerun narrow slices if constraints change.
- **Agent hallucination risk:** Strict “no-new-facts” rule for Writer; Red-Team checks per paragraph.

## 11) Milestones (initial)
- **M0.1 Scaffolding (this week):** repo initialized; templates + prompts added.
- **M0.2 First vertical slice:** “Standards compliance — simdjson” through G2.
- **M0.3 Matrix pass (all libs):** first draft of FeatureMatrix across core dimensions.
- **M0.4 Draft chapters → Red-Team:** performance + DX first.
- **M1.0 Report v1.0:** tag and Notion snapshot.

---

**Status:** v0.1 updated to reflect MD + CSV paired artifact decision.
