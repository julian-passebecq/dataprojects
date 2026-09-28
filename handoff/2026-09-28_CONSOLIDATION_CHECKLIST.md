# 2026-09-28 — consolidation checklist before Codex Tech Lead pass

This file is the final PM/brainstorm archival checklist before handing technical leadership to Codex.

## Archived

- [x] DataPass V4 product boundary.
- [x] Common Semantic Engine concept.
- [x] DataPass Hop V3 reuse path.
- [x] file role taxonomy.
- [x] operation taxonomy.
- [x] evidence/provenance levels.
- [x] static/declared/captured/observed lineage separation.
- [x] deterministic analysis before AI.
- [x] AI uncertainty-resolution contract.
- [x] Common Catalog concept.
- [x] tool/extension/service catalogue.
- [x] architecture pattern catalogue.
- [x] operation knowledge catalogue.
- [x] workload profile.
- [x] performance/cost-driver model.
- [x] semantic Git diff opportunity.
- [x] Prototype Cloud role.
- [x] Fabric V1 first vertical.
- [x] scenario feature/subvariant model.
- [x] monitoring/quality/dev-effort trade-offs.
- [x] Hub role.
- [x] Factory local-only role.
- [x] no fake Spark.
- [x] no mandatory Spark.
- [x] no cloud hosting/MotherDuck requirement.
- [x] no Kubernetes/k3s core.
- [x] no MinIO/S3 emulator by default.
- [x] optional FastAPI/Redis/Docker only when needed.
- [x] dbt nested DAG below global Factory DAG.
- [x] dlt ingestion boundary.
- [x] DuckDB/DuckLake/local Parquet preference.
- [x] Polars/Pandas/scikit-learn roles.
- [x] Mosaic/workbench donor inventory.
- [x] ducklabms_code donor inventory.
- [x] Contoso donors.
- [x] fastapi-fabric donor.
- [x] fastapispark explicit Factory exclusion.
- [x] Duckle prior ADR discovered.
- [x] Duckle vs Mosaic/hybrid architecture gate.
- [x] existing GitLab Factory placeholder discovered.
- [x] GitHub/GitLab Cloud Studio duplicate discovered.
- [x] Cloudiagram removed from DataPass core galaxy.
- [x] Cloudiagram ideas to harvest.
- [x] DataPass Front / datapass-studio deferred.
- [x] FOIL client/scenario fixtures identified.
- [x] current constellation naming conflict recorded.
- [x] Codex Tech Lead responsibilities.
- [x] PM Opus role separated from tech lead.
- [x] coding-agent work packet format.
- [x] proposed technical lot hierarchy.
- [x] cross-host repository authority map.

## Explicitly unresolved for Codex

These are not omissions; they are deliberate tech-lead decisions.

1. **DataPass naming migration**
   - existing constellation uses "Datapass" for ducklabms_code coding/interview product;
   - latest direction reserves DataPass for datapass-vscode V4.

2. **Common-engine ownership migration**
   - datapass-vscode currently syncs some schemas/examples/knowledge to datapass-vscode-common;
   - Codex must define one-way ownership/versioning without circular sync.

3. **Prototype Cloud authority**
   - active GitLab implementation vs older GitHub repo;
   - Codex must formalize write authority/archive/mirror policy.

4. **Factory canonical repository**
   - existing GitLab `juliandatapass-group/datapass-factory` is a placeholder;
   - do not create another repo before ADR.

5. **Factory lower execution architecture**
   - Duckle adapter-first;
   - extracted Mosaic/FactoryLab engine;
   - hybrid.
   - Must be decided by spike-backed `ADR-FACTORY-EXECUTION-001`.

6. **Workbench extraction package boundary**
   - Mosaic vs ducklabms donor code;
   - package/repo ownership and dependency direction.

7. **Catalog ownership/versioning**
   - current DataPass toolkit;
   - dataprojects VS Code/tool catalogue;
   - new common catalog.

8. **Exact Fabric V1 scenario schemas**
   - finalize after Common IR/catalog IDs exist.

## Out of scope for current technical lead implementation wave

- Cloudiagram product integration;
- PPTX/publication work;
- DataPass Front / Streamlit-like product;
- hosted Factory;
- MotherDuck;
- Kubernetes/k3s runtime;
- distributed scheduler;
- fake Spark;
- Airflow as Factory core;
- Meltano as Factory core;
- provider-cloud deployment.

## Required Codex deliverables before PM starts broad coding wave

- [ ] live-state repo audit report;
- [ ] architecture dependency map;
- [ ] ADR set;
- [ ] Common Semantic IR spec;
- [ ] package/repo ownership map;
- [ ] Factory execution spike report + ADR;
- [ ] lot/sub-lot/feature decomposition;
- [ ] work-packet templates filled for Wave 1;
- [ ] parallelization/merge dependency graph;
- [ ] security/trust-boundary spec;
- [ ] migration/backward-compatibility plan;
- [ ] CI/test matrix;
- [ ] explicit list of deferred work.

## Handoff read order

1. `CLAUDE.md`
2. `handoff/2026-09-28_CODEX_TECH_LEAD_MASTER_BRIEF.md`
3. `handoff/2026-09-28_REPOSITORY_AUTHORITY_MAP.md`
4. `handoff/2026-09-28_DATAPASS_V4_FACTORY_MASTER.md`
5. `handoff/2026-09-28_REPOSITORY_REUSE_INVENTORY.md`
6. `registry/proposals/2026-09-28-datapass-v4-factory.json`
7. technical branch/PR in `datapass-vscode-common`
8. live product repos and their own AGENTS/CLAUDE/handoffs

This checklist marks the PM/brainstorm consolidation as complete enough for the tech-lead architecture pass.
