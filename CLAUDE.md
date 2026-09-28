# Claude entry point — 2026-09-28 DataPass V4 / Prototype Cloud / Factory plan

This branch contains a **proposed constellation update** based on Julian Passebecq's 2026-09-28 architecture decisions.

**Authorship note:** the analysis was produced in ChatGPT by **GPT-5.6 Sol**, not GPT-6.

## Authority

- This repository remains the global portfolio/constellation authority.
- Individual product repositories remain implementation/test truth.
- The existing main registry predates the 2026-09-28 DataPass V4/Factory redesign and therefore contains naming/scope conflicts that must be reconciled deliberately.
- Do not silently overwrite the existing six-product registry from this handoff.

## Read first

1. [handoff/2026-09-28_CODEX_TECH_LEAD_MASTER_BRIEF.md](handoff/2026-09-28_CODEX_TECH_LEAD_MASTER_BRIEF.md)
2. [handoff/2026-09-28_REPOSITORY_AUTHORITY_MAP.md](handoff/2026-09-28_REPOSITORY_AUTHORITY_MAP.md)
3. [handoff/2026-09-28_CONSOLIDATION_CHECKLIST.md](handoff/2026-09-28_CONSOLIDATION_CHECKLIST.md)
4. [handoff/2026-09-28_DATAPASS_V4_FACTORY_MASTER.md](handoff/2026-09-28_DATAPASS_V4_FACTORY_MASTER.md)
4. [registry/proposals/2026-09-28-datapass-v4-factory.json](registry/proposals/2026-09-28-datapass-v4-factory.json)
3. Current main [registry/constellation.json](registry/constellation.json) and relevant product entries.
4. Technical specifications on branch **plan/v4-semantic-engine-factory** of [julian-passebecq/datapass-vscode-common](https://github.com/julian-passebecq/datapass-vscode-common):
   - handoff/V4_MASTER_HANDOFF.md
   - handoff/V4_COMMON_ENGINE_SPEC.md
   - handoff/V4_FACTORY_SPEC.md
   - handoff/V4_ORCHESTRATION_DECISION.md
   - handoff/V4_FABRIC_V1.md
   - handoff/V4_EXECUTION_PLAN.md

## Critical boundaries

- DataPass V4 = repo intelligence/control-plane evolution of **julian-passebecq/datapass-vscode**.
- Prototype Cloud = architecture alternatives/catalog consumer in **datapass-vscode-cloud**.
- Hub = lightweight capability/tool router in **datapass-vscode-hub**.
- Factory = local executable-prototype product. A private GitLab placeholder already exists at **juliandatapass-group/datapass-factory**; do not create another repo before the tech-lead ADR.
- Mosaic remains a separate learning product/donor; extract only reusable workbench infrastructure.
- Cloudiagram is deferred to later publication/PPTX consumption; not central to the first implementation wave.
- Contoso Data Studio and Contoso Data Generator are major Factory donors/fixtures.
- **Factory V1 must not contain fake Spark or a Spark simulator.**
- **Kubernetes is not required by Factory V1.**
- **Factory V1 lower execution is an OPEN TECH-LEAD GATE.** Codex must compare Duckle adapter-first, extracted Mosaic/FactoryLab control flow, and a hybrid before choosing. The Factory semantic DAG remains above dlt/dbt/Polars/sklearn and dbt is a nested transformation DAG.
- **Duck-first local minimalism:** DuckDB/local Parquet first, DuckLake when lakehouse semantics matter; no MinIO/local S3 emulator by default.
- Docker Compose is optional and only for service-style scenarios.
- Deterministic analysis comes before AI.
- Native provider files remain authoritative.
- Do not execute arbitrary client code during DataPass discovery.
- Never present local Factory metrics as observed cloud metrics.

## Naming conflict to resolve

The existing main registry currently uses the product name **Datapass** for the coding/interview studio in **ducklabms_code**. The 2026-09-28 plan uses **DataPass V4** for the repo-intelligence/control-plane extension in **datapass-vscode**.

This is a real conflict. Do not hide it.

Before updating main, prepare a focused naming/scope migration proposal, for example:

- reserve **DataPass** for the control-plane/repo-intelligence product and rename the learning product; or
- give the control-plane a distinct permanent product name.

Julian's latest conversation strongly treats **datapass-vscode** as “DataPass classic” moving to V4, so this should be the default proposal, but the registry migration should still be explicit and reviewed.
