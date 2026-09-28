# 2026-09-28 — Codex Tech Lead master brief

Authoring context: product/brainstorm consolidation by **GPT-5.6 Sol** in ChatGPT. This is not a claim that GPT-6 produced the plan.

## Mission

Codex is the **technical lead / architecture lead**, not the PM and not the bulk implementation team.

Codex must turn the product vision into an implementation architecture that another PM can schedule and multiple coding agents can execute safely.

The goal is not to rewrite every repository. The goal is to establish a coherent shared engine and clear product boundaries, then migrate vertically.

## Required first action: reconcile live truth

Before proposing final architecture:

1. fetch all repositories listed in the repository-authority map;
2. inspect current branches, open PRs/MRs, CI, agent instructions and handoffs;
3. distinguish implementation truth from planning truth;
4. identify duplicate GitHub/GitLab repositories and choose authority explicitly;
5. produce a current-state dependency graph;
6. list all existing reusable code before creating a new subsystem.

Do not assume the SHA values in planning docs are still current.

## Final product intent to preserve

### DataPass V4

Purpose: understand the real Git project.

Responsibilities:
- repository/project structure;
- Git history and semantic diff;
- file classification;
- artifact role;
- milestones;
- deterministic static analyzers;
- static/declarative/captured/observed lineage;
- findings;
- readiness;
- WorkloadProfile;
- tools/capabilities;
- architecture/project variants;
- uncertainty packets for optional AI.

Discovery does not execute arbitrary client code.

### Prototype Cloud

Purpose: architecture design alternatives.

Responsibilities:
- architecture pattern catalogue;
- subvariants/features;
- Fabric V1 first;
- developer/operations effort;
- monitoring patterns;
- cost/performance drivers;
- required capabilities/extensions;
- AI proposal contract using validated catalogue IDs.

No cloud provisioning.

### Factory

Purpose: **100% local executable data-project prototype**, editable, observable and demonstrable.

Final hard boundaries:
- local only;
- no hosting product;
- no MotherDuck requirement;
- no fake Spark;
- no Spark simulator;
- no Kubernetes/k3s core dependency;
- no MinIO/S3 emulation by default;
- no mandatory Docker;
- DuckDB/local Parquet first;
- DuckLake only when lakehouse semantics add value;
- dbt Core/dbt-duckdb;
- dlt;
- Polars/Pandas;
- scikit-learn;
- optional FastAPI/Redis/Docker only when a scenario needs those semantics.

Global Factory DAG must sit **above dbt**. dbt remains an expandable transformation/model sub-DAG.

### Hub

Purpose: route the user to the correct product/tool/extension/capability.

Hub does not duplicate analyzers, provider clients or the catalogue.

### Outside current core

- Mosaic remains a learning product/donor.
- Cloudiagram is **not a DataPass galaxy product** for this implementation wave. Harvest its good architecture ideas only.
- DataPass Front / Streamlit-like front is deferred.
- Mongoku remains optional portfolio/read-model work.
- provider-specific editors remain specialist tools.

## Critical unresolved architecture gate: Factory execution foundation

Do **not** greenfield an ETL/orchestration engine before resolving this gate.

There are at least three credible paths.

### Option A — Duckle adapter-first

External repo: `slothflowlabs/duckle`.

Existing prior decision in `datapasscontrol/control/decisions/duckle-factorylab.json` says Duckle is the primary lower-layer candidate pending integration spike.

Verified useful characteristics:
- MIT OR Apache-2.0;
- visual React/@xyflow pipeline authoring;
- plain Git-friendly pipeline JSON;
- DuckDB execution;
- DuckLake I/O;
- generated SQL/plan;
- status/rows/timings/previews;
- column lineage;
- run history;
- control-flow nodes;
- scheduling;
- dbt execution;
- headless runner/server;
- MCP;
- local/single-machine design.

Required spike:
- translate a minimal Factory pipeline into Duckle JSON;
- run source/filter/select/join/sink;
- run DuckLake sink/source;
- obtain per-node rows/timings/errors;
- obtain generated SQL/plan and preview;
- obtain lineage or document gaps;
- test dbt integration boundary;
- test one control-flow node;
- map security/process boundary;
- measure packaging/startup cost;
- list exact Fabric-like semantics not representable.

Default strategy if sufficient: **adapter**, not fork.

### Option B — extract/evolve Mosaic/FactoryLab local engine

Existing donor code:
- `datapass-mosaic-vscode/runtime/factorylab/engine.py`;
- `runtime/datapass_runtime/factory_workspace.py`;
- `SharedGraphCanvas`;
- `FactoryPipelines.tsx`;
- `PipelineSurface.tsx`;
- related code in `ducklabms_code` and Fabric migration sources.

Existing semantics include dependencies, success/failure/completed edges, retries, timeout, If/Switch/ForEach/Until, child pipelines, parameters, variables, run state and local Workspace boundary.

Required spike:
- isolate control-flow kernel from learning/simulation code;
- replace one simulated activity with real DuckDB execution;
- execute dbt as a nested group;
- normalize run receipts;
- verify cancellation/timeout/subprocess isolation;
- estimate maintenance cost.

### Option C — hybrid

Factory semantic/control-flow layer remains ours, while Duckle provides data-flow execution/connectors/generated SQL/preview/lineage.

This may be the strongest option if the boundary stays small.

### Decision rule

Codex must write an ADR with evidence after the spikes.

Do not select:
- Duckle because it has many features;
- our own engine because we already wrote it;
- Dagster/Airflow because they are famous.

Choose the smallest maintainable architecture that satisfies local-only Factory semantics while keeping the Common Semantic IR authoritative.

Dagster/Airflow/Hop remain possible adapters/importers, not assumed core.

## Frontend / workbench reuse gate

Do not create another graph/editor framework.

Audit and compare:
- `datapass-mosaic-vscode` workbench/grid/DAG surfaces;
- `ducklabms_code/apps/web/src/foundation/GraphCanvas.tsx`;
- `WorkbenchSurface.tsx`;
- Fabric migration-source pipeline UI in ducklabms_code;
- DataPass Hop source/understanding split-pane;
- active Cloud Studio webview patterns.

Expected target is a reusable workbench package/pattern:
- pane layout;
- graph canvas;
- file/code pane;
- details pane;
- table/data preview;
- nested dbt DAG;
- run state;
- layout persistence.

Keep domain schemas separate: project DAG, file-understanding graph and dbt DAG are related but not one universal mutable graph.

## Cloudiagram ideas to harvest, not product-integrate

GitLab Cloudiagram stays outside the DataPass galaxy.

Reusable architecture principles:
- one canonical model; imports compile into it rather than creating parallel truth;
- stable IDs;
- designed vs inferred vs captured-plan vs supplied/observed evidence;
- source hints are not automatically lineage;
- preview/review/apply boundaries;
- revision/hash guards;
- public/private projection discipline;
- bounded parsers/importers;
- architecture -> task -> model/join/code -> execution drill-down;
- scoped presentation/export later;
- human approval before publication/verification;
- AI/MCP may propose but not self-approve.

Do not make Cloudiagram a dependency.

## DataPass Front / Streamlit-like idea

Current GitHub `julian-passebecq/datapass-studio` is essentially a placeholder.

Decision:
- do not add a fifth core product now;
- leave the ultra-fast Streamlit/Next-like front outside the current execution plan;
- a future **DataPass Front** may consume Common Engine/Factory APIs for rapid demos;
- do not block V4/Factory on it.

Existing Streamlit projects such as `foil-streamlit-wind-3d-lcoe` may be scenario/UI donors only, never shared authority.

## Required technical architecture output from Codex

Codex must produce:

### 1. Architecture Decision Records

At minimum:
- common-engine ownership and package boundaries;
- GitHub/GitLab authority/mirroring;
- DataPass naming migration;
- Factory canonical repo;
- Factory execution foundation (Duckle vs extracted engine vs hybrid);
- workbench extraction boundary;
- semantic IR versioning;
- analyzer plugin contract;
- run receipt/evidence model;
- catalogue ownership/versioning;
- AI proposal/uncertainty contract;
- security/process execution boundary.

Each ADR:
- context;
- options;
- decision;
- evidence;
- rejected alternatives;
- consequences;
- rollback/revisit condition.

### 2. Target architecture

Must include:
- repo topology;
- package boundaries;
- runtime processes;
- dependency direction;
- trust boundaries;
- data/control flow;
- local filesystem layout;
- API/IPC contracts;
- versioning;
- state ownership;
- testing strategy.

### 3. Technical lots and sub-lots

Use a hierarchy:

```text
LOT
  SUB-LOT
    FEATURE
      WORK PACKET
```

Every feature must list:
- owning repo;
- branch;
- dependencies;
- contract/schema;
- files/modules expected;
- implementation logic;
- non-goals;
- unit tests;
- integration/UI tests;
- migration;
- acceptance;
- rollback;
- merge dependency.

### 4. Code logic specifications

For implementation agents, describe logic precisely enough that they do not invent architecture.

Example:
- inputs;
- validation;
- state machine;
- algorithms;
- error behavior;
- concurrency/cancellation;
- persistence;
- security limits;
- emitted evidence/receipts;
- exact interface boundaries.

Do not prescribe line-by-line code when an existing module already provides the behavior; point to donor code and expected adaptation.

### 5. Integration graph

Codex must identify which lots can execute in parallel and which are blocking.

No PM-style staffing assignment is required from Codex.

## Recommended technical lot structure

Codex may revise after audit, but start from:

### LOT 0 — truth reconciliation / ADR gates
- repo authority;
- naming;
- Factory repo;
- Duckle/existing-engine spikes;
- common ownership.

### LOT 1 — Common Semantic Core
- Artifact/Role/Milestone/Operation;
- Dataset/Field;
- Evidence/Basis;
- Lineage;
- Finding;
- Metric;
- Workload;
- uncertainty;
- IDs/versioning.

### LOT 2 — DataPass V4 compatibility + analyzers
- datapass.understanding adapter;
- file classifier;
- SQL analyzer;
- Python/PySpark static analyzer;
- ipynb;
- dbt manifest;
- Fabric pipeline;
- TMDL/BIM;
- semantic Git diff.

### LOT 3 — Common Catalog
- tools/extensions/capabilities;
- operations;
- architecture patterns;
- practices;
- monitoring;
- findings rules;
- cost/performance drivers;
- source/as-of/versioning.

### LOT 4 — Prototype Cloud / Fabric V1
- scenario contract;
- feature toggles;
- 2–3 proposal UX;
- workload inputs;
- AI validated proposal JSON;
- monitoring/tool recommendations;
- CU/cost driver representation.

### LOT 5 — reusable workbench
- graph canvas;
- panes;
- code/source navigation;
- nested graph;
- data preview;
- run status;
- layout persistence.

### LOT 6 — Factory execution foundation
Only after the ADR/spike:
- semantic Factory DAG;
- chosen lower execution architecture;
- run receipts;
- dbt nested DAG;
- dlt;
- DuckDB/DuckLake;
- Python/Polars/Pandas/sklearn;
- cancellation/retry/timeout;
- local security.

### LOT 7 — Factory scenarios
- Contoso retail;
- wind-turbine;
- generated files;
- optional FastAPI;
- optional Redis;
- optional Docker Compose;
- investor/demo reset/run flow.

### LOT 8 — Hub
- capability registry consumer;
- installed tool discovery;
- route/open commands;
- DataPass/Prototype/Factory/native-tool handoff.

### LOT 9 — hardening
- performance bounds;
- large repos;
- schema migrations;
- security;
- Windows acceptance;
- VSIX packaging;
- CI;
- donor attribution/licenses.

### LATER / NOT CURRENT LOT
- Cloudiagram publication/PPTX integration;
- DataPass Front;
- MotherDuck/cloud hosting;
- Kubernetes;
- distributed execution.

## Agent operating model

Recommended split:

### Codex = Tech Lead

Use the strongest available Codex reasoning setting for the architecture pass.

Responsibilities:
- source audit;
- ADRs;
- dependency graph;
- technical lots;
- interface design;
- work packets;
- spikes;
- integration review;
- architecture drift detection.

Codex should avoid becoming the project manager.

### PM = Opus 5.5

Responsibilities:
- convert Codex technical graph into staffing waves;
- assign coding agents;
- manage worktrees/branches;
- enforce prerequisites;
- track status/blockers;
- coordinate integration order;
- request Codex review when architecture changes;
- decide when to stop a coding wave and re-plan.

### Implementation agents = Opus 5.5 medium

Give each agent a bounded packet:
- one repo/worktree;
- one technical feature;
- explicit contracts;
- donor files;
- acceptance/tests;
- no authority to change global architecture.

If a packet requires an interface change, agent returns a design question instead of silently changing the contract.

### Integration reviewer

Codex should review:
- contract changes;
- cross-repo coupling;
- data migrations;
- security/process boundaries;
- new dependencies;
- final integration PRs.

PM can review scheduling/completion, but should not substitute for tech-lead architecture review.

## Work-packet template

```text
ID
Lot / sub-lot
Owning repo
Base ref
Feature branch
Goal
Why
Dependencies
Existing donor code
Contracts consumed
Contracts produced
Implementation logic
Files/modules likely touched
Security/trust constraints
Non-goals
Unit tests
Integration/E2E tests
Acceptance
Artifacts/evidence
Migration/backward compatibility
Rollback
Open questions
Blocked-by
Blocks
```

## Final instruction to Codex

Do not optimize for the number of repositories or features delivered.

Optimize for:
- one shared vocabulary;
- one authority per piece of state;
- reuse before rewrite;
- deterministic evidence before AI;
- local simplicity;
- bounded dependencies;
- narrow vertical slices;
- truthful claims;
- reversible migrations.
