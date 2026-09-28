
# 2026-09-28 — repository inventory and reuse notes

This focused inventory complements, and does not replace:

- registry/repository-inventory.json
- registry/repo-cartography.json
- registry/tooling.json
- registry/vscode-tool-catalog.json

Claude must consult those files before creating another repository or rebuilding a capability.

## Global control

### julian-passebecq/dataprojects
Global constellation authority. Owns product boundaries/categories/status, not implementation truth.

### julian-passebecq/datapasscontrol
Detailed DataPass-family historical/sub-registry. Its own README says dataprojects is the global authority.

## Proposed central family

### julian-passebecq/datapass-vscode
Target: DataPass V4 — Git/repository intelligence and control plane.

Preserve: graph/project bridge, Git, options/scenarios, project sheet, toolkit/toolchain, readiness, work orders and DataPass Hop.

Add incrementally: shared semantic engine, file roles, milestones, deterministic analyzers, static lineage, findings, uncertainty/AI questions and semantic Git diff.

### julian-passebecq/datapass-vscode-common
Target: provider-neutral contracts/packages and common Catalog.

Caveat: existing V3 schemas/examples/knowledge are partly synchronized from datapass-vscode. Avoid circular ownership; migrate deliberately.

Technical planning branch: plan/v4-semantic-engine-factory.

### julian-passebecq/datapass-vscode-cloud
Target: Prototype Cloud — architecture pattern/scenario/subvariant comparison using Common Catalog and project WorkloadProfile. No cloud provisioning.

### julian-passebecq/datapass-vscode-hub
Target: lightweight capability/product/extension router. No duplicate analyzer or catalog.

### proposed julian-passebecq/datapass-vscode-factory
Not created yet. Target: real local executable prototypes.

Factory V1 stack:
DuckDB, optional DuckLake, Parquet, dlt, dbt Core/dbt-duckdb, Polars, Pandas, scikit-learn, optional FastAPI, optional Redis, optional Docker Compose, optional dbt Charts and later optional MotherDuck.

Factory V1 explicitly excludes:
fake Spark, Spark simulation, mandatory Spark, mandatory Airflow, Kubernetes, Kafka and mandatory Docker.

## Major Factory donors

### julian-passebecq/datapass-mosaic-vscode
Learning product and major workbench donor.

Reuse candidates:
- flexible React grid/panes;
- runtime client/protocol and loopback token model;
- DuckDB/DuckLake catalog surfaces;
- result tables/query history;
- graph/DAG rendering primitives;
- layout persistence;
- trusted local Python UX patterns.

Do not port:
- SparkLab/fake Spark;
- simulated Spark metrics;
- Practice/Interview;
- grading/missions;
- provider-learning simulations as Factory core.

### julian-passebecq/contoso-data-studio
Primary retail Factory donor/fixture.

Existing useful assets:
- deterministic scenarios;
- seed/scale;
- generator and file hashes;
- reproducible run manifests;
- run comparison;
- DuckLake service;
- DuckDB exploration;
- dbt-duckdb;
- dbt tests;
- dbt Charts;
- Gold KPI previews.

### julian-passebecq/Contoso-Data-Generator-V2
Large generator/parity/evidence donor.

Extract narrowly:
- deterministic generation;
- truth manifests;
- output-format support;
- scenario/scale concepts;
- parity/evidence patterns.

Do not port its Spark/Airflow/Minikube/Kubernetes stack wholesale into Factory V1.

### julian-passebecq/Contoso_Data_Fabric
Older Fabric/Contoso donor/reference. Reuse only a specific superior asset; do not revive duplicate scope.

## Runtime/service experiments

### julian-passebecq/fastapispark
Current purpose: fake Spark learning runtime with DuckDB real results plus simulated Spark stages/tasks/partitions/shuffle/spill.

Decision: DO NOT REUSE IN FACTORY. Julian explicitly removed fake Spark.

Possible remaining use: Mosaic/learning/reference only.

### julian-passebecq/fastapi-fabric
Fabric/Data Factory learning/simulation backend.

Potential donor patterns:
- strict pipeline schema;
- dependency/run/cancel state;
- bounded expression handling.

Do not make it Factory's universal executor.

### julian-passebecq/datapass-airflow-runner
Known empty/near-empty. No Factory V1 dependency.

### slothflowlabs/duckle
External candidate already tracked by the older FactoryLab registry. Inspect before reinventing a lower execution layer, but adopt only if it fits the new typed Factory DAG, local-first and security boundaries.

## Visualization / publication donors

### GitLab julianpassebecq/cloudiagram
Later publication/drill-down/PPTX consumer, not immediate critical path.

Known V2 state at proposal time:
- branch feat/cloudiagram-v2-desktop-ai-documents
- SHA 2941d9c3f0c1e21f5bac3a9c297e3f35bdbdd79e
- MR !1 draft/open
- pipeline successful.

Useful existing capabilities include detail authoring, document/source inputs, BIM/TMDL/notebook/script detail, logical joins, scoped drill-down, editable PPTX, Electron PDF/publication, CLI/MCP.

### julian-passebecq/VizLens
Architecture-pattern donor: deterministic local extraction before optional AI, evidence IDs, constrained AI contracts and privacy-aware local companion. Not a runtime dependency.

### julian-passebecq/Fluent2_J_Viz
Potential visual/UI donor. Inspect only for a concrete need.

### julian-passebecq/DrawCloud and Fluent2_J_CloudArchi
Older cloud/architecture donors. Reference only unless a unique component is demonstrated.

## Fabric/tooling donors

### julian-passebecq/fabricdatapasstoolbox
Real-Fabric VS Code companion experiment. Consolidate proven actions into Catalog/Hub; avoid a second generic Fabric shell.

### julian-passebecq/fabric-toolbox_J
Large Fabric ops/toolbox fork/donor. Reuse proven scripts/actions/monitoring patterns through Catalog/Hub.

External tools already tracked by dataprojects include FabricStudio, OneLake-VSCode, microsoft/fabric-toolbox and microsoft/fabric-cicd. Prefer specialist/vendor tooling rather than duplicating provider clients.

## Power BI / semantic-model donors

### julian-passebecq/powerbi_enhanced_dev
Broad Power BI engineering IDE donor. Inspect specialized capability before reuse; not the global shell.

### julian-passebecq/TabularEditor_J
Specialized TE2/TOM donor/tool. Keep external/integrated; do not rebuild advanced TOM editing in Hub/DataPass.

External data-goblin Power BI agent/toolbox projects are already cataloged. Use as optional tools/references, not code to repackage wholesale.

## DataPass-family experiments

### julian-passebecq/datapass-studio
Older/minimal. Inspect only for a concrete reusable asset.

### julian-passebecq/codex-datapass-bridge
Private agent-exchange experiment. Compare with current V3 work orders/exchange before reuse.

### datapass-vscode-helper / datapass-vscode-vsix / datapass-vscode-codex-auto / codex-datapass-vsixtest / fakeclient repos
Helpers/tests/experiments, not products by default.

### julian-passebecq/foil-v1-vscode-datapass
Potential real-project qualification fixture. Keep FOIL-specific business/scientific logic outside Common Engine.

## Separate families

AtlasNote/AtlasCode/AtlasMongo and FOIL domain repositories are separate families. Do not expand V4/Factory scope just because they contain potentially reusable code.

## Existing global registry conflict

Current dataprojects main lists these core products:
- Datapass (ducklabms_code coding/interview studio)
- CaseLab
- Airflow Lab
- Fabric Factory Lab
- Contoso Data Studio
- PBI/Semantic Lab

The 2026-09-28 proposal instead introduces the central developer galaxy:
- DataPass V4 = datapass-vscode
- Prototype Cloud
- Factory
- Hub

Claude must prepare an explicit migration table before changing constellation.json. This is not a cosmetic rename.

Likely outcome from Julian's latest wording:
- reserve DataPass for the classic datapass-vscode product evolving to V4;
- rename/reclassify the coding/interview product;
- decide whether old Fabric Factory Lab remains a learning product or donates to broader Factory;
- keep Contoso as a useful scenario/product/donor;
- keep focused learning products separate.

## Full inventory rule

Before creating a repo or claiming no donor exists:

1. read registry/repository-inventory.json;
2. read registry/repo-cartography.json;
3. read registry/tooling.json;
4. read registry/vscode-tool-catalog.json;
5. search Julian's GitHub repositories;
6. inspect the candidate donor's actual source and tests.

Implementation source wins for what currently works.
dataprojects wins for reviewed product boundaries until a new proposal is merged.
