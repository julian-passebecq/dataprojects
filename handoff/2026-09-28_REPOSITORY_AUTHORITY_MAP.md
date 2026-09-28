# 2026-09-28 — repository authority map for DataPass V4 / Factory program

This document exists so Codex does not confuse mirrors, donors, placeholders and implementation authorities.

## Authority hierarchy

1. `dataprojects` owns reviewed product/constellation boundaries.
2. Each application repo owns implementation/test truth.
3. `datapass-vscode-common` is the proposed common technical-contract/catalog home, but current V3 sync ownership must be migrated deliberately.
4. `datapasscontrol` is a historical/detailed sub-registry and contains useful older decisions; it is not the current global authority.
5. External repos are donors/dependencies only; pin versions/licenses before integration.

---

## Core / proposed core products

### DataPass V4
**GitHub:** `julian-passebecq/datapass-vscode`  
Current main snapshot at this consolidation: `ccb2d8913681729d29e322a2f526b3bcf21fb3b3`.

Role:
- classic DataPass evolves to repo intelligence/control plane.

Preserve:
- project bridge;
- graph;
- options/scenarios;
- sheet;
- Git/worktrees/PR/CI;
- toolchain;
- toolkit;
- work orders/exchange;
- DataPass Hop / datapass.understanding.

### Common Engine / Catalog
**GitHub:** `julian-passebecq/datapass-vscode-common`  
Main snapshot: `6afdac03b28a42054ba04bdd4579b63ee9ea1ec2`.  
Planning PR: #23, branch `plan/v4-semantic-engine-factory`.

Role:
- shared semantic contracts;
- analyzer contracts;
- Catalog;
- workload/findings/perf/cost types;
- Factory contracts;
- eventual workbench extraction target.

Caveat:
- V3 schemas/examples/knowledge are currently partly synced from datapass-vscode. Codex must design migration to one-way ownership before moving them.

### Prototype Cloud / Cloud Studio
There are **two repositories** and they are not automatic mirrors.

**Active GitLab implementation:**  
`juliandatapass-group/datapass-vscode-cloud`  
Project ID 86939337.  
This is the active DataPass Cloud Studio codebase and contains the detailed 2026-09-28 Architecture Inspector handoff.

**GitHub repository:**  
`julian-passebecq/datapass-vscode-cloud`  
Main snapshot: `fcedc911719c996bd1885a0d42eb8be8be359e16`.

The active GitLab README explicitly states there is no automatic GitHub/GitLab mirror.

Codex must:
- diff the two;
- designate GitLab as active implementation authority unless newer evidence contradicts it;
- decide whether GitHub becomes archived/reference/manual mirror;
- never write features independently to both.

Target role:
- source-derived technical inspection;
- architecture pattern bank;
- Fabric V1 alternatives/subvariants;
- workload-aware comparison;
- native-tool guidance;
- no provisioning.

### DataPass Hub
**GitHub:** `julian-passebecq/datapass-vscode-hub`  
Main snapshot: `7b716843ef5600c24b85dfe9704e5edeae66ef11`.

Role:
- capability/tool/product router;
- no duplicate parser/catalog/provider client.

### Factory
An existing repo already exists.

**GitLab placeholder:**  
`juliandatapass-group/datapass-factory`  
Project ID 86942381.  
Current state: default GitLab README only, no implementation.

Therefore:
- **do not create `datapass-vscode-factory` until Codex makes an ADR**;
- preferred first option is to use/rename this existing GitLab repository if the product boundary fits.

Related client placeholders:
- `foil-lab/datapass-factory-foil` — GitLab project 86942393;
- `foil-lab/datapass-factory-foil-bridge` — GitLab project 86942882.

Both currently contain only default README content. Treat as placeholders/client-scope candidates, not implemented Factory.

---

## Major implementation donors

### datapass-mosaic-vscode
**GitHub:** `julian-passebecq/datapass-mosaic-vscode`  
Snapshot: `60192bd59c50e6a04b513c5e72d8042ca47917fa`.

Role:
- learning product;
- major Factory/workbench donor.

Important donors:
- SharedGraphCanvas;
- FactoryPipelines;
- PipelineSurface;
- flexible panes;
- runtime protocol;
- local data surfaces;
- `runtime/factorylab/engine.py`;
- `runtime/datapass_runtime/factory_workspace.py`.

Do not port:
- fake Spark/SparkLab;
- learning grading/missions;
- provider simulations as runtime truth.

### ducklabms_code
**GitHub:** `julian-passebecq/ducklabms_code`  
Snapshot: `c1ebf0d982fbcb2d22564c2bc04ab290630cfba7`.

This is a very large donor and is also involved in the old naming conflict where the existing constellation called a coding/interview product “Datapass”.

Important reusable areas:
- `apps/web/src/foundation/GraphCanvas.tsx`;
- `WorkbenchSurface.tsx`;
- Monaco/notebook patterns;
- pipeline compiler/runner;
- dbt runner/worker;
- execution/local jobs;
- DuckLake/local-data code;
- Fabric migration sources;
- analytics/dbt/model/chart workbench pieces.

Do not treat the whole repo as a dependency. Extract narrowly.

### fastapi-fabric
**GitHub:** `julian-passebecq/fastapi-fabric`.

Current role:
- standalone Fabric Factory Lab semantic/simulation backend;
- pipeline CRUD/validation;
- parameters/variables;
- dependencies;
- expression evaluation;
- deterministic simulated runs;
- run/cancel API.

Reuse:
- Fabric/ADF semantic contracts and validation;
- expression/control-flow ideas;
- API patterns.

Do not automatically expand it into the generic Factory execution engine.

### contoso-data-studio
**GitHub:** `julian-passebecq/contoso-data-studio`  
Snapshot: `5faa9c47c694cea35471d8a7aef991faaac3fb12`.

Primary retail Factory fixture/donor:
- deterministic data;
- DuckDB/DuckLake;
- dbt;
- tests;
- charts;
- KPI/explorer patterns.

### Contoso-Data-Generator-V2
**GitHub:** `julian-passebecq/Contoso-Data-Generator-V2`.

Reuse selectively:
- deterministic generator;
- scenario/scale;
- manifests/evidence;
- Parquet/CSV output patterns.

Do not wholesale import Spark/Airflow/Kubernetes-related paths.

### Contoso_Data_Fabric
**GitHub:** `julian-passebecq/Contoso_Data_Fabric`.

Older upstream/reference generator. Use only if an asset is superior and license/provenance allows reuse.

---

## External lower-layer candidate

### Duckle
**External GitHub:** `slothflowlabs/duckle`.

Current reviewed state:
- open-source MIT OR Apache-2.0;
- local/self-hosted ETL platform;
- React/@xyflow canvas;
- Git-friendly pipeline JSON;
- DuckDB engine;
- DuckLake support;
- generated SQL/plans;
- previews;
- rows/timings/status;
- lineage;
- run history;
- control flow;
- dbt;
- scheduling;
- headless runner/server.

Historical accepted-direction record:
`julian-passebecq/datapasscontrol/control/decisions/duckle-factorylab.json`.

Codex must perform an adapter-first spike **before approving a greenfield generic ETL executor**.

Duckle is a candidate lower execution layer, not a DataPass product.

---

## Historical coordination / architecture records

### datapasscontrol
**GitHub:** `julian-passebecq/datapasscontrol`  
Snapshot: `48c10804dea0cc6d9ebbf77932ea310ed36d6002`.

Read for:
- old FactoryLab boundaries;
- Duckle decision;
- shared assets;
- donor extraction plan;
- workstreams.

Do not use as global authority if it conflicts with dataprojects.

### dataprojects
**GitHub:** `julian-passebecq/dataprojects`  
Main snapshot before this planning branch: `3dd61a749b2fd0f5ea859cf54d0b12a31053542c`.

Global constellation authority.

Current planning branch:
`plan/datapass-v4-factory-constellation`.

---

## Client / realistic fixtures

### foil-v1-vscode-datapass
**GitHub private:** `julian-passebecq/foil-v1-vscode-datapass`.

Use as a DataPass real-project qualification fixture. Keep FOIL-specific scientific/business logic outside Common Engine.

### foil-fabric-v1
**GitHub private:** `julian-passebecq/foil-fabric-v1`.

Cloud Studio handoffs already cite this as a realistic Fabric fixture with batch medallion / realtime / Power BI examples. Synthetic/non-measured numbers must stay labelled as such.

### foil-streamlit-wind-3d-lcoe
**GitHub private:** `julian-passebecq/foil-streamlit-wind-3d-lcoe`.

Possible wind/demo UI/domain donor only. Do not make it Common Engine/Factory authority.

### GitLab FOIL Factory placeholders
- `foil-lab/datapass-factory-foil`;
- `foil-lab/datapass-factory-foil-bridge`.

Currently placeholders; do not claim implementation.

---

## Cloudiagram — ideas donor only, explicitly outside the DataPass galaxy

**GitLab:** `julianpassebecq/cloudiagram`  
Project ID 86939635.

Known V2 working branch from this planning cycle:
`feat/cloudiagram-v2-desktop-ai-documents`.

Do not list Cloudiagram as a central DataPass V4 product.

Harvest concepts only:
- canonical-model discipline;
- evidence/provenance levels;
- bounded importers;
- stable IDs;
- macro/micro drilldown;
- review/apply;
- revision/hash guards;
- source hints != lineage;
- privacy/public projection;
- AI proposes / human approves.

Cloudiagram remains an independent future publication/PPTX product.

---

## Fabric / Power BI / tooling donors

### fabricdatapasstoolbox
GitHub: `julian-passebecq/fabricdatapasstoolbox`.

### fabric-toolbox_J
GitHub: `julian-passebecq/fabric-toolbox_J`.

### powerbi_enhanced_dev
GitHub: `julian-passebecq/powerbi_enhanced_dev`.

### TabularEditor_J
GitHub: `julian-passebecq/TabularEditor_J`.

### VizLens
GitHub: `julian-passebecq/VizLens`.

### Fluent2_J_Viz
GitHub: `julian-passebecq/Fluent2_J_Viz`.

### DrawCloud / Fluent2_J_CloudArchi
Older diagram/architecture donors.

Rule:
- Catalog/Hub should point to/reuse specialist tools where appropriate;
- do not rebuild provider IDEs in DataPass.

---

## Experiments / helpers — inspect only for a concrete need

- `julian-passebecq/codex-datapass-bridge`;
- `datapass-vscode-helper`;
- `datapass-vscode-vsix`;
- `datapass-vscode-codex-auto`;
- `codex-datapass-vsixtest`;
- `datapass-codex-test`;
- `datapass-codex-fakeclient*`;
- `datapass-airflow-runner` (currently empty/near-empty);
- `datapass-vs-code-archive`.

These are not products by default.

---

## Explicitly excluded from Factory core

### fastapispark
GitHub: `julian-passebecq/fastapispark`.

Reason:
- fake/simulated Spark concepts;
- Julian explicitly removed fake Spark from Factory.

May remain learning/Mosaic donor only.

### Kubernetes / k3s
No core repo/runtime.

May later exist as a separate architecture lab/adaptor, but Factory local V1 does not need it.

### Streamlit/DataPass Front
**GitHub:** `julian-passebecq/datapass-studio`.

Current repo is effectively a placeholder (README only).

Decision:
- defer;
- do not include as a core product now;
- future “DataPass Front” may consume Common/Factory APIs for ultra-fast prototypes.

---

## GitHub/GitLab duplicate rule

Whenever the same product name exists on both:
1. compare latest code/CI/handoffs;
2. designate exactly one write authority;
3. mark the other mirror/archive/reference;
4. never implement independent features in both;
5. document whether sync is manual/automated.

Current known duplicate requiring action:
- `datapass-vscode-cloud` GitHub vs GitLab; active evidence currently favors GitLab.

---

## Before creating any new repo

Codex must search:
- dataprojects registry;
- datapasscontrol historical registry;
- GitHub user repos;
- GitLab owned projects;
- donor trees;
- open PRs/MRs.

No new repository should be created just because a handoff used a proposed name.
