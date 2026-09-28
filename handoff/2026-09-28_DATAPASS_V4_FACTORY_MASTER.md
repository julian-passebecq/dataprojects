# 2026-09-28 — DataPass V4 / Prototype Cloud / Factory master handoff

Authoring context: Julian Passebecq + ChatGPT  
Analysis model: **GPT-5.6 Sol**  
Important: **not GPT-6**

Status: **proposal / planning branch**, not yet merged into the global registry.

This file is deliberately exhaustive. It records the path of the discussion, the reasoning behind the new architecture, current repositories, reuse decisions, product boundaries and execution order so Claude can continue without reconstructing the entire conversation.

---

# 1. Why this handoff exists

Julian has a large number of overlapping data-engineering, BI, Fabric, local-runtime, visualization and VS Code experiments.

Several threads converged:

1. understand a cloud/data Git project at every level;
2. explain every file meaningfully;
3. visualize architecture and lineage;
4. compare alternative architectures;
5. understand cost/performance/capacity implications;
6. route the developer toward the right extension/tool;
7. create a very fast local prototype that actually runs;
8. later present it cleanly to clients/investors.

Previous projects each solved a portion:

- DataPass V3: project/Git/control plane + Hop file understanding;
- Cloud Studio: cloud/native-tool guidance;
- Mosaic: flexible local workbench/labs;
- Contoso Data Studio: local DuckDB/DuckLake/dbt data platform;
- Cloudiagram: architecture/detail/PPTX publication;
- multiple FastAPI services: isolated simulation/runtime ideas;
- Hub/control registries: portfolio/tool routing.

The new goal is not to merge everything into one application.

The goal is to establish a **large shared semantic/catalog foundation** and give each product one narrow responsibility.

---

# 2. Important authority conflict discovered during this handoff

The current dataprojects main registry was created earlier and currently defines six core learning/data products.

In that registry:

- “Datapass” currently means the coding/interview product in ducklabms_code.
- “Fabric Factory Lab” means a Fabric/ADF-style learning/simulation product.
- Contoso is the local analytics platform.

Julian’s latest 2026-09-28 discussion uses names differently:

- **DataPass classic / DataPass V4** = julian-passebecq/datapass-vscode, the project/Git/control-plane extension;
- **Factory** = a broad local executable cloud/data prototype product, not only a Fabric learning lab;
- Mosaic becomes peripheral/learning rather than central;
- Cloudiagram becomes later publication, not central.

This is a real naming/scope conflict.

Do not silently modify registry/constellation.json.

Before merging a new constellation, prepare an explicit migration decision.

The latest user intent strongly indicates:

> reserve the “DataPass V4” direction for datapass-vscode, because Julian explicitly asked what “DataPass classique” should become in V4.

A likely migration is therefore:

- rename/refocus the older coding/interview “Datapass” product;
- promote datapass-vscode as the primary DataPass repo-intelligence/control-plane product;
- broaden/redefine Factory separately from the old Fabric Factory Lab.

But this must be reviewed in a dedicated registry PR.

---

# 3. Chronological reasoning path

## 3.1 Initial Cloudiagram problem

Julian originally wanted more than architecture diagrams.

He wanted:

~~~text
architecture
 -> pipeline
 -> task
 -> data model
 -> join
 -> code
 -> execution detail
 -> partitions / metrics
~~~

The practical UX idea:

- click a component;
- see its task;
- click the task;
- see tables and joins;
- click a table;
- see schema;
- click a notebook milestone;
- see the relevant source;
- understand performance concepts;
- export selected detail to PPTX.

Cloudiagram V2 work was built around a semantic detail model and editable presentation.

This proved that the drill-down UI is useful.

But it also proved that a presentation product cannot reliably explain arbitrary project files on its own.

Another layer must first understand the Git repo.

---

## 3.2 Own format instead of Apache Hop as foundation

Apache Hop was considered as inspiration for visual ETL.

The conclusion:

- do not make Apache Hop the canonical model;
- do not make it a mandatory dependency;
- use provider/engine adapters into our own semantic representation.

The internal idea became:

~~~text
native sources
  SQL
  PySpark
  ADF
  Fabric
  dbt
  notebook
  Hop
      |
      v
DataPass semantic representation
~~~

Then any consumer can visualize/publish it.

---

## 3.3 Discovery of DataPass Hop V3

Review of datapass-vscode showed that DataPass V3 already has a strong concept called DataPass Hop.

Current datapass.understanding contains:

- one native file target;
- SHA-256;
- language;
- steps;
- line ranges;
- inputs;
- outputs;
- columns;
- links;
- joins;
- provenance;
- milestone labels.

The existing UX can synchronize code lines and visual steps.

This directly matches a large part of Julian’s “left code / right explanation” request.

Important current design:

- DataPass does not execute the native file to explain it;
- client AI can prepare the understanding JSON;
- DataPass validates it;
- file hash marks it stale if code changed.

Conclusion:

> V4 should build on DataPass Hop rather than replace it.

But V4 should move from “AI writes all understanding” toward:

~~~text
deterministic parser
 -> static semantics
 -> uncertainties
 -> optional AI enrichment
 -> reviewed explanation
~~~

---

## 3.4 The missing abstraction: classify every file

Julian identified the critical missing idea:

> We cannot answer “what does every file do?” unless we have a common vocabulary for what cloud/data files can represent.

A notebook is not infinitely unique at the semantic level.

Useful project/file roles include:

- ingestion;
- extraction;
- loading;
- cleaning;
- normalization;
- enrichment;
- aggregation;
- curation;
- quality;
- reconciliation;
- serving;
- semantic modeling;
- reporting;
- orchestration;
- infrastructure;
- configuration;
- testing;
- monitoring;
- deployment;
- exploration;
- feature engineering;
- training;
- scoring;
- API/service;
- generation;
- utility.

A notebook/file can have:

- primary role;
- secondary roles;
- layer;
- inputs;
- outputs;
- milestones;
- operations.

Example:

~~~text
silver_orders.py

kind:
  notebook

technology:
  PySpark

primary role:
  enrichment

secondary:
  cleaning
  quality

layer:
  silver

inputs:
  bronze.orders
  dim.customer

output:
  silver.orders
~~~

This classification must be common across providers.

---

## 3.5 The second abstraction: common operations

Provider-specific syntax maps to common operations.

Examples:

~~~text
Spark join()
SQL JOIN
Dataflow merge
Hop lookup
~~~

all represent a logical join.

Initial operation vocabulary:

- read;
- write;
- filter;
- project/select;
- rename;
- cast;
- derive;
- join;
- lookup;
- aggregate;
- window;
- sort;
- deduplicate;
- union;
- pivot/unpivot;
- explode;
- merge/upsert;
- validate/assert;
- branch/loop/trigger/call;
- send/receive;
- train/predict.

Physical execution details are separate evidence.

---

## 3.6 Lineage must be honest

The discussion explicitly separated:

### static lineage

Derived from code/parser.

### declared lineage

Supplied by project/AI/config.

### captured lineage/plan

Supplied by provider/native artifacts.

### observed lineage/runtime

Supported by actual run evidence.

No source-order arrow should be called runtime lineage.

Every fact/edge needs basis/evidence.

Recommended basis vocabulary:

- declared;
- static;
- inferred;
- estimated;
- illustrative;
- captured;
- observed.

---

## 3.7 DataPass V4 becomes repo intelligence

The emerging definition:

> DataPass V4 understands what is actually in the Git project.

It should answer:

- what files/artifacts exist?;
- what role does each file play?;
- what milestones does it contain?;
- what operations occur?;
- what datasets are read/written?;
- what static lineage is justified?;
- what problems/risks can be detected?;
- what information is unknown?;
- what changed semantically in Git?;
- which official extension/tool should the developer use next?

DataPass should remain:

- local-first;
- Git-aware;
- non-executing during discovery;
- provider-native;
- optional-AI;
- explicit about uncertainty.

---

# 4. Common Engine emerged as the foundation

The shared semantic engine should expose a common IR:

~~~text
Artifact
 -> Role
 -> Milestone
 -> Operation
 -> Dataset / Field
 -> Lineage
 -> Evidence
 -> Execution Hint
 -> Metric
 -> Finding
 -> WorkloadProfile
 -> Performance Driver
 -> Cost Driver
 -> Uncertainty
~~~

This engine must be usable by:

- DataPass V4;
- Prototype Cloud;
- Hub;
- Factory;
- later Cloudiagram;
- potentially other products.

It should not depend on VS Code APIs.

The detailed specification is on branch:

**julian-passebecq/datapass-vscode-common / plan/v4-semantic-engine-factory**

Read:

- handoff/V4_COMMON_ENGINE_SPEC.md
- handoff/V4_EXECUTION_PLAN.md

---

# 5. Three catalog layers

Current DataPass Toolkit already has useful knowledge about:

- tools;
- extensions;
- CLIs;
- MCP;
- prices/free tiers;
- install routes;
- useWhen;
- avoidWhen;
- side effects;
- recipes;
- verification dates.

Do not create a new “Toolkit extension” unless a product boundary later demands it.

Instead evolve the common Catalog into three conceptual layers.

## Tool/service/extension catalog

Question:

> What tool should I use?

## Architecture pattern catalog

Question:

> How can this system be built?

Examples:

- lakehouse medallion;
- warehouse ELT;
- hybrid lakehouse/warehouse;
- batch BI;
- streaming;
- CDC;
- document pipeline;
- ML pipeline.

## Operation knowledge catalog

Question:

> What does this transformation mean and what problems/performance concerns can it create?

Examples:

- join;
- window;
- aggregate;
- merge;
- deduplicate;
- partitioning.

---

# 6. Prototype Cloud

Existing repo:

**julian-passebecq/datapass-vscode-cloud**

Current repo is an independent VS Code Cloud Studio prototype.

Target role:

> propose and compare architecture alternatives using Common Engine project/workload facts + Catalog knowledge.

Inputs:

- current DataPass project analysis;
- WorkloadProfile;
- user constraints;
- Catalog;
- optional AI answers.

Outputs:

- 2–3 architecture scenarios;
- subvariants/feature toggles;
- assumptions;
- questions;
- developer effort;
- operational effort;
- monitoring;
- performance drivers;
- cost/capacity drivers;
- required tools/extensions.

No cloud provisioning.

---

# 7. Alternatives are not only A/B/C

DataPass already supports decisions/options/scenarios.

Keep that.

Add feature-level choices.

Example Fabric scenario:

~~~text
Fabric Lakehouse
 -> Bronze
 -> Silver
 -> Gold
 -> Semantic model
~~~

Possible feature choices:

- dbt on/off;
- Direct Lake vs Import;
- full vs incremental;
- Copy vs Shortcut;
- notebook vs SQL vs mixed;
- separate Gold layer;
- materialized tables vs views;
- monitoring profile;
- quality profile;
- refresh staggering;
- delivery/Git profile.

Each option must expose consequences.

Do not create one hidden “best” score.

---

# 8. WorkloadProfile

Scenario comparison cannot work from architecture names alone.

Need structured workload facts:

- dataset rows;
- bytes;
- file counts;
- growth/day;
- refresh frequency;
- retention;
- concurrency;
- latency target;
- number/size of joins;
- semantic refresh;
- consumers.

Values should have basis/source.

DataPass project sheet already contains part of this.

V4 should formalize a shared projection instead of inventing a second uncontrolled project file.

---

# 9. Cost/performance principles

The project must never output magic precise cost numbers from weak evidence.

Use drivers.

Examples:

- bytes/run;
- runs/day;
- concurrency;
- query duration;
- notebook duration;
- refresh overlap;
- capacity tier;
- storage;
- requests;
- egress.

Native units stay native:

- Fabric CU;
- Databricks DBU;
- compute-hour;
- vCPU-hour;
- GB-month.

Never invent a universal CU -> DBU conversion.

Outputs:

- range;
- assumptions;
- confidence;
- missing data;
- source/date for prices.

---

# 10. Monitoring knowledge

Monitoring should be attached to architecture patterns.

Examples:

Pipeline:

- failure;
- duration;
- retries;
- moved rows/files.

Notebook:

- failure;
- duration;
- input/output volume if available.

Semantic:

- refresh failure;
- refresh duration;
- freshness.

Data quality:

- row counts;
- nulls;
- key uniqueness;
- freshness;
- volume anomalies.

Capacity:

- overlap;
- throttling;
- peak windows.

Catalog provides the recipe.

Hub routes to the actual provider monitoring tool.

---

# 11. Hub

Existing repo:

**julian-passebecq/datapass-vscode-hub**

Current repo is very small.

Target:

> lightweight capability/tool/product router.

Examples:

Selected semantic model:

~~~text
Understand
 -> DataPass

Edit semantic model
 -> Power BI Authoring / specialized tool

Browse Fabric
 -> official/community Fabric extension

Compare architecture
 -> Prototype Cloud

Build local proof
 -> Factory
~~~

Selected notebook:

~~~text
Understand file
 -> DataPass Hop/Semantic lens

Run real cloud notebook
 -> official provider extension/tool

Prototype local equivalent
 -> Factory
~~~

Hub should not:

- own analyzers;
- own catalog data independently;
- execute arbitrary commands from catalog;
- duplicate provider UIs.

Use allowlisted extension commands/routes.

---

# 12. Factory pivot

Julian then made another important change.

Instead of keeping Mosaic or Cloudiagram central, create a local Factory product.

Factory goal:

> build a local, cheap, fast, editable, executable proof of a cloud/data project.

This is different from a learning simulator.

Factory should let an investor/client see:

- generated data;
- ingestion;
- transformations;
- data model;
- ML;
- lineage;
- actual local run metrics;
- code;
- outputs;
- dashboard.

---

# 13. Factory V1 stack

Final V1 decisions:

Core:

- Python;
- DuckDB;
- Parquet.

Optional lakehouse:

- DuckLake.

Ingestion:

- dlt.

Global orchestration:

- **Dagster OSS** as the reference Factory V1 orchestrator;
- Factory owns a provider-neutral semantic DAG above dbt;
- dbt remains an expandable transformation/model sub-DAG.

Transformation:

- dbt Core + dbt-duckdb;
- DuckDB SQL;
- Polars;
- Pandas.

ML:

- scikit-learn.

Services where needed:

- FastAPI;
- Redis.

Packaging:

- Docker Compose optional.

Charts:

- simple local charts;
- dbt Charts optional.

Sharing later:

- MotherDuck optional.

---

# 14. Final explicit removal: fake Spark

Earlier discussion considered using local engines plus a Spark-behavior simulator.

Julian explicitly removed that.

Final decision:

> **Factory V1 has no fake Spark.**

Do not import:

- fastapispark;
- Mosaic SparkLab;
- simulated Spark stages;
- simulated shuffle;
- virtual Spark clusters.

Existing fake-Spark products may remain learning/reference products.

Factory uses real local execution on:

- DuckDB;
- DuckLake;
- Polars;
- Pandas;
- sklearn.

If real Spark is ever needed later, add an explicit real Spark adapter.

---

# 14.5 Local minimalism / Duck-first rule

The local prototype should use the smallest number of moving pieces that still demonstrates the project.

Preferred order:

1. DuckDB.
2. local Parquet.
3. DuckLake when lakehouse semantics are genuinely useful.
4. Polars/Pandas.
5. dbt-duckdb.
6. dlt.
7. sklearn.
8. Dagster.
9. FastAPI only for a real service/API boundary.
10. Redis only for real queue/cache/stream/state semantics.
11. Docker Compose only for service processes.
12. MotherDuck only as optional sharing.

Explicitly **do not add MinIO/local S3 emulation by default**. DuckLake + local Parquet is the preferred V1 lakehouse story.

Do not add Postgres, Kafka, Grafana, MLflow, Kubernetes or another service simply to imitate cloud infrastructure.

---

# 15. Kubernetes decision

Factory V1 does not require Kubernetes.

No:

- minikube;
- kind;
- k3d;
- Helm cluster path as normal setup.

Docker Compose is enough for optional services.

Kubernetes may become a future specialized target.

---

# 16. FastAPI decision

FastAPI is not “the data type layer”.

Use FastAPI when the prototype needs an API/service boundary.

Examples:

- IoT telemetry API;
- business service;
- ML scoring endpoint;
- webhook;
- generator API.

A simple dbt/DuckDB project should not start FastAPI.

---

# 17. Redis decision

Redis is optional.

Use for:

- cache;
- queue;
- stream;
- shared temporary state;
- run progress.

Example:

~~~text
turbine telemetry
 -> FastAPI
 -> Redis Stream
 -> dlt
 -> DuckLake
~~~

Do not start Redis when not needed.

---

# 18. Factory orchestration

dlt is ingestion, not the general orchestrator.

dbt owns the transformation/model DAG, but the Factory project needs a **global DAG above dbt**.

Final V1 decision:

> **Dagster OSS is the reference orchestration/runtime adapter.**

Factory still owns a strict provider-neutral semantic DAG with stable IDs, dependencies, nested groups, evidence/source references and normalized receipts. Dagster executes it.

Hierarchy:

~~~text
Factory global DAG
  generator
    -> dlt
    -> dbt group
         -> dbt internal model DAG
    -> Polars/Pandas
    -> sklearn
    -> publish/demo
~~~

Why Dagster:

- local/open-source;
- visible asset/job graph;
- designed around data assets;
- strong fit above dbt/Python work;
- compatible with dlt integration;
- no Kubernetes requirement;
- avoids rebuilding a scheduler.

Airflow remains a future adapter/import route for real client projects, not the Factory V1 runtime.

Meltano remains a cataloged alternative/importer, not a Factory core dependency.

Factory must show its own DAG in the Workbench; Dagster's UI is an optional deep operational view.

Full technical decision is in `datapass-vscode-common/handoff/V4_ORCHESTRATION_DECISION.md`.

---

# 19. Factory runtime variants

Same logical project can have local implementation variants.

Examples:

~~~text
CSV -> Pandas -> Parquet
~~~

~~~text
Parquet -> DuckDB -> dbt -> Gold
~~~

~~~text
Parquet -> Polars -> DuckLake
~~~

~~~text
FastAPI -> Redis -> dlt -> DuckLake
~~~

Factory can compare actual local metrics:

- duration;
- rows;
- files;
- memory if measurable;
- steps;
- container count;
- setup complexity.

These metrics are local observations only.

---

# 20. Extract Mosaic’s common workbench

Repo:

**julian-passebecq/datapass-mosaic-vscode**

Mosaic already has:

- React grid workbench;
- code/data/chart panes;
- DuckDB/DuckLake runtime;
- query history;
- Polars;
- table previews;
- DAG/pipeline views;
- runtime client with loopback token;
- layout persistence.

Extract a generic package:

~~~text
@datapass/workbench-core
~~~

Target content:

- grid/split layout;
- pane registration;
- source/editor bridge;
- code pane;
- SQL pane;
- notebook/text pane;
- table preview;
- chart pane;
- graph/DAG pane;
- lineage mini-map;
- run status;
- runtime protocol;
- layout persistence.

Do not extract into Factory:

- Practice;
- Interview;
- grading;
- course missions;
- SparkLab;
- fake Spark;
- simulated Airflow;
- simulated provider labs.

Mosaic remains separate.

---

# 21. Contoso donors

## contoso-data-studio

Current useful implementation:

- deterministic retail scenarios;
- generator manifests;
- file hashes;
- reproducibility;
- run comparison;
- DuckLake;
- DuckDB;
- dbt-duckdb;
- tests;
- dbt Charts;
- KPIs;
- React/Fluent UI.

Use as first Factory fixture/donor.

## Contoso-Data-Generator-V2

Very large donor.

It has more advanced generation/parity/runtime ideas.

Important warning:

it also contains:

- Spark;
- Airflow;
- Minikube/Kubernetes;
- other paths that are outside Factory V1.

Do not port that stack wholesale.

Extract:

- data-generation scenarios;
- deterministic truth manifests;
- output formats;
- parity/evidence patterns where useful.

---

# 22. Contoso Factory scenario

Retail V1:

~~~text
generate
 -> inspect
 -> Bronze
 -> dbt Silver
 -> dbt Gold
 -> KPIs
 -> charts
~~~

Factory adds:

- DAG/run status;
- semantic understanding pane;
- lineage;
- run metrics;
- scenario comparison;
- optional ML.

---

# 23. Wind Factory scenario

A major requested investor demo.

Entities:

- sites;
- turbines;
- telemetry;
- weather;
- maintenance;
- alerts.

Local path:

~~~text
generators
   |
   v
FastAPI optional
   |
Redis optional
   |
dlt
   |
DuckLake Bronze
   |
dbt / DuckDB
   |
Silver / Gold
   |
Polars features
   |
sklearn
   |
predictions / anomaly score
   |
dashboard
~~~

Also provide a no-Docker path:

~~~text
generator
 -> Parquet
 -> dlt/dbt
 -> DuckDB/DuckLake
 -> Polars
 -> sklearn
~~~

---

# 24. Factory should emit real local evidence

Run receipt:

- step;
- status;
- duration;
- rows;
- output files/tables;
- model metrics;
- source hash;
- environment=local;
- basis=observed.

Do not call this cloud evidence.

Later Prototype Cloud may use it only through an explicit model.

---

# 25. Factory snapshot

Factory can emit a sanitized read-model snapshot.

Potential fields:

- project;
- scenario;
- run;
- steps;
- datasets;
- lineage;
- metrics;
- ML metrics;
- findings.

Future consumers:

- Cloudiagram;
- Mongoku;
- reports;
- investor deck generation.

Snapshot is not canonical project authority.

---

# 26. Cloudiagram role changed

GitLab repo exists and is healthy.

Latest known:

- repo: gitlab.com/julianpassebecq/cloudiagram;
- branch: feat/cloudiagram-v2-desktop-ai-documents;
- SHA: 2941d9c3f0c1e21f5bac3a9c297e3f35bdbdd79e;
- MR !1 draft;
- pipeline success.

Cloudiagram already has:

- manual/detail authoring;
- BIM/TMDL/notebook/script/Spark-plan-related detail import;
- drill-down;
- editable PPTX;
- Electron publication;
- MCP/CLI paths.

Do not throw it away.

But it is no longer on the immediate critical path.

Later role:

> consume sanitized semantic/run snapshots and produce polished drill-down/PPTX/PDF.

---

# 27. Other donors discovered

## fastapispark

Repo:

julian-passebecq/fastapispark

Current purpose:

fake Spark learning runtime using DuckDB + simulated Spark-like stages/metrics.

Decision:

**do not reuse in Factory**.

Reason:

Julian explicitly removed fake Spark.

Keep only as Mosaic/learning/reference if desired.

---

## fastapi-fabric

Repo:

julian-passebecq/fastapi-fabric

Current purpose:

standalone deterministic Fabric/Data Factory learning/simulation API.

Possible reuse:

- strict pipeline contract ideas;
- run-state API;
- activity validation;
- expression handling patterns.

Do not make it Factory’s general executor by default.

Factory should remain provider-neutral.

---

## VizLens

Repo:

julian-passebecq/VizLens

Useful donor patterns:

- deterministic local extraction before AI;
- optional AI;
- constrained request/response contracts;
- local companion service;
- strict privacy boundary;
- evidence IDs.

This philosophy aligns strongly with V4.

Do not turn it into a core dependency.

---

## TabularEditor_J

Specialized semantic-model donor/tool.

Keep specialized external.

Hub/DataPass should integrate/launch rather than reimplement advanced TOM editing.

---

## powerbi_enhanced_dev / PbiBench

Broad Power BI engineering IDE donor.

Potential use:

- semantic-model engineering patterns;
- Power BI workflows.

Do not use as global shell.

---

## fabricdatapasstoolbox / fabric-toolbox_J

Real-Fabric/toolbox donors.

Use Catalog/Hub to expose proven capabilities.

Do not create duplicate generic Fabric extensions if official/community tools already solve the need.

---

## datapass-studio

Very small/older repo.

Inspect only if a concrete reusable asset is identified.

Do not assume it is the new Factory.

---

## datapass-airflow-runner

Currently empty/near-empty.

No reason to depend on it for Factory V1.

---

# 28. dataprojects existing registry donors

Current dataprojects already tracks:

- ducklabms_code;
- leetcodedataeng;
- datainterview;
- deepnotejul;
- Fluent2_J_CodeLab;
- Fluent2_J_Formation;
- sqldubr;
- Fluent2_J_CloudArchi;
- fastapispark;
- fastapi-fabric;
- contoso-data-studio;
- Contoso-Data-Generator-V2;
- Contoso_Data_Fabric;
- fabricdatapasstoolbox;
- fabric-toolbox_J;
- powerbi_enhanced_dev;
- TabularEditor_J;
- FOIL-specific repos;
- Atlas family;
- control-plane experiments.

Claude must consult registry/repo-cartography.json before creating a new donor/replacement.

---

# 29. Tool/extension catalog should absorb current VS Code catalog work

dataprojects already has registry/vscode-tool-catalog.json with useful decisions such as:

- use official/community Fabric extensions;
- do not build another OneLake explorer;
- use Microsoft Fabric toolbox assets;
- keep specialized Power BI tools external;
- official Databricks extension as primary client;
- use OpenTofu/Terraform/Kubernetes/Docker peer tools directly;
- Grafana code/tooling integrations.

This should inform the new Common Catalog.

Do not discard this work.

The long-term goal is not to have two incompatible catalogs:

- dataprojects VS Code catalog;
- DataPass toolkit/catalog.

Claude should create a migration/consolidation plan.

Likely target:

- global portfolio metadata stays in dataprojects;
- operational reusable tool/catalog schema lives in datapass-vscode-common;
- dataprojects references that catalog rather than duplicating volatile technical facts.

---

# 30. DataPass V4 semantic Git opportunity

Once files map to a common IR, DataPass can compare commits semantically.

Examples:

~~~text
join:
  inner -> left

data:
  + customer_segment

quality:
  + not-null check

materialization:
  view -> table

pipeline:
  + task quality_gate
~~~

This is a major future differentiator.

Keep it in DataPass, not Factory.

---

# 31. Findings engine

Potential deterministic findings:

- possible cross join;
- LEFT JOIN effectively turned into INNER by filter;
- SELECT * on wide/joined data;
- large-data collect risk;
- repartition(1)-style anti-pattern when source size supports concern;
- full refresh despite low daily change;
- semantic-model ambiguous relationship;
- missing key/grain test;
- overlapping refresh schedules;
- missing failure path.

Each finding:

- severity;
- confidence;
- evidence;
- missing evidence;
- verification steps.

Never turn a heuristic into certainty.

---

# 32. AI role across the galaxy

AI should not be the foundation.

DataPass:

- deterministic parser first;
- AI only for unresolved business meaning/dynamic references.

Prototype Cloud:

- AI proposes catalog-valid scenarios/features;
- engine validates.

Factory:

- no AI required to run;
- AI may later help author local prototype files.

Hub:

- no AI required.

Cloudiagram:

- AI optional for authoring proposals.

---

# 33. First Fabric V1 vertical

Detailed spec lives in datapass-vscode-common handoff/V4_FABRIC_V1.md.

Important decision families:

- Lakehouse vs Warehouse;
- notebook/Spark vs SQL vs mixed transformation;
- medallion depth;
- full vs incremental;
- Direct Lake vs Import;
- pipeline vs notebook-chain orchestration;
- dbt on/off;
- Copy vs Shortcut;
- Gold materialization;
- refresh/capacity scheduling;
- monitoring profile;
- quality profile;
- Git/deployment profile.

Do not create decorative variants.

Each choice must affect actual developer/ops work.

---

# 34. Example subvariant: dbt

dbt OFF:

- fewer tools;
- less setup;
- faster onboarding;
- more custom conventions;
- less standardized dependency/test metadata.

dbt ON:

- explicit model DAG;
- tests;
- manifests;
- clearer SQL project structure;
- extra setup/CI/tooling.

Do not claim dbt automatically reduces CU.

Only changed work/materialization/incremental behavior can change capacity usage.

---

# 35. Example subvariant: full vs incremental

Inputs:

- total data;
- daily changes;
- refresh;
- late arrivals;
- key/watermark support.

Full:

- simpler;
- potentially more processing.

Incremental:

- less processing potential;
- more correctness/state/backfill complexity.

Show consequences, not a hidden winner.

---

# 36. Capacity/CU comparison

Do not try to predict exact CU from source code alone.

Use drivers:

- bytes/run;
- frequency;
- duration;
- concurrency;
- refresh overlap;
- query workload.

Output:

- low/medium/high pressure;
- estimated range where model supports it;
- assumptions;
- missing evidence;
- confidence.

Later compare with observed provider metrics.

---

# 37. Monitoring profiles

Minimum:

- failures;
- semantic refresh failure;
- capacity/throttle alert where available.

Standard:

- durations;
- volumes;
- freshness;
- quality checks;
- overlap.

Enhanced:

- deeper capacity/performance;
- trend history;
- transform-level metrics.

Hub points to actual monitoring tool.

---

# 38. Common workbench UX

Target reusable workbench:

~~~text
+----------------+-------------------------+------------------+
| project tree   | native editor           | understanding    |
|                |                         |                  |
| files/tasks    | code / SQL / notebook   | role/milestones  |
|                |                         | lineage/findings |
+----------------+-------------------------+------------------+
| mini data/DAG/lineage map                                  |
+------------------------------------------------------------+
~~~

This fulfills the original request:

> pane left/center file, pane right decomposition, bottom mini map.

---

# 39. Source-to-milestone behavior

A long notebook/file should be broken into a small number of meaningful milestones.

Process:

~~~text
deterministic segmentation
 -> operation grouping
 -> role inference
 -> optional AI naming
~~~

Example:

~~~text
1 setup
2 load source
3 clean
4 enrich customer
5 aggregate KPIs
6 quality
7 write
~~~

Click milestone:

- highlight source;
- scope lineage;
- show operations;
- show findings.

---

# 40. Product constellation proposal

If adopted, the central working galaxy becomes:

~~~text
                DataPass Common Engine
                         |
       +-----------------+------------------+
       |                 |                  |
       v                 v                  v
   DataPass V4      Prototype Cloud       Factory
   repo truth       architecture          local execution
       \                 |                  /
        \                |                 /
         +----------- DataPass Hub --------+
                    routing/tools
~~~

Peripheral:

- Mosaic = learning + workbench donor;
- Cloudiagram = later publication;
- Contoso = donor/fixture;
- Mongoku = optional portfolio/read-model.

---

# 41. Concrete repo roles

## julian-passebecq/datapass-vscode

Target:
DataPass V4.

Keep:

- Git;
- bridge;
- graph;
- project;
- options;
- sheet;
- toolkit;
- readiness;
- work orders;
- Hop;
- variants.

Add:

- common semantic engine;
- analyzers;
- file roles;
- milestones;
- static lineage;
- findings;
- AI uncertainties;
- semantic Git diff;
- capability routing.

---

## julian-passebecq/datapass-vscode-common

Target:
common contracts/catalog/shared packages.

Planning branch already created:

**plan/v4-semantic-engine-factory**

Docs already created there:

- CLAUDE.md;
- handoff/V4_MASTER_HANDOFF.md;
- handoff/V4_COMMON_ENGINE_SPEC.md;
- handoff/V4_FACTORY_SPEC.md;
- handoff/V4_FABRIC_V1.md;
- handoff/V4_EXECUTION_PLAN.md.

Important:

current schemas/examples/knowledge are partially sync-owned by datapass-vscode.

Do not create circular ownership.

---

## julian-passebecq/datapass-vscode-cloud

Target:
Prototype Cloud.

Refactor toward:

- common Catalog;
- current-project/workload import;
- architecture patterns;
- feature toggles;
- scenario comparison;
- AI proposal JSON;
- Factory handoff.

No provisioning.

---

## julian-passebecq/datapass-vscode-hub

Target:
lightweight router.

Current repo is tiny.

Build only after common capability contract.

---

## new Factory repo

Recommended:

**julian-passebecq/datapass-vscode-factory**

Do not create until naming/registry decision is confirmed.

Use:

- workbench-core;
- Common Engine;
- local runtime.

---

## julian-passebecq/datapass-mosaic-vscode

Target:
learning product.

Extract generic workbench base.

Do not port fake Spark.

---

## julian-passebecq/contoso-data-studio

Target:
donor + retail Factory fixture.

---

# 42. Execution order

Do not build all products in parallel.

Safe order:

1. reconcile registry naming;
2. common semantic-core;
3. datapass.understanding compatibility;
4. deterministic SQL analyzer;
5. first DataPass V4 file-understanding UX;
6. Python/PySpark static analyzer;
7. notebook analyzer;
8. catalog V2;
9. Fabric V1 catalog;
10. WorkloadProfile;
11. Prototype Cloud scenario refactor;
12. workbench-core extraction;
13. Factory skeleton;
14. Factory DAG;
15. Contoso generator integration;
16. DuckDB/DuckLake;
17. dbt;
18. Polars/Pandas/sklearn;
19. dlt;
20. optional FastAPI/Redis/Docker Compose;
21. Wind fixture;
22. Hub;
23. semantic Git diff;
24. richer provider analyzers;
25. cost/perf engine;
26. later Cloudiagram snapshot/PPTX.

Detailed gates:
datapass-vscode-common / handoff/V4_EXECUTION_PLAN.md.

---

# 43. First task Claude should actually execute

Do not begin with Factory UI.

First:

## A. Reconcile naming and ownership

Produce an explicit proposed registry diff:

- current dataprojects product names;
- proposed new names/scopes;
- what is renamed vs new;
- what remains learning/peripheral.

Do not merge without review.

## B. Build Common Semantic Core alpha

In datapass-vscode-common.

Types:

- Artifact;
- Role;
- Milestone;
- Operation;
- Dataset;
- Lineage;
- Evidence;
- Finding;
- Metric;
- Uncertainty.

Unit tests.

No VS Code.

## C. Map datapass.understanding V1

Compatibility adapter.

Prove existing Hop can migrate incrementally.

Only then touch consumer products.

---

# 44. Key anti-sprawl rules

Do not:

- create one mega extension;
- create a new catalog in every repo;
- create a new semantic model in Factory;
- create a new lineage format in Prototype;
- copy Mosaic wholesale;
- port fake Spark;
- add Kubernetes V1;
- make Airflow mandatory;
- make Docker mandatory;
- make AI mandatory;
- duplicate official Fabric/OneLake/Databricks tooling;
- reimplement Tabular Editor;
- reimplement dbt Charts if integration is enough;
- treat local metrics as cloud metrics;
- confuse source-order with lineage;
- overwrite V3 contracts without compatibility.

---

# 45. Final target experience

A developer opens a real Fabric project.

DataPass:

~~~text
silver_orders.py
  role: enrichment
  layer: silver

milestones:
  load
  clean
  join customer
  calculate KPI
  quality
  write

data:
  bronze.orders + dim.customer -> silver.orders

findings:
  one possible issue
  two unknown metrics

AI:
  one business-intent question
~~~

Prototype Cloud:

~~~text
Current project workload:
  ...

Scenario A:
  Lakehouse/mixed
  Direct Lake
  incremental
  no dbt

Scenario B:
  Lakehouse/dbt
  incremental

Scenario C:
  Warehouse SQL

Each shows:
  required work
  monitoring
  capacity/cost drivers
  manual tasks
  tools
~~~

User selects scenario.

Factory:

~~~text
Build local prototype

generator
 -> dlt
 -> DuckLake
 -> dbt
 -> Polars
 -> sklearn
 -> dashboard
~~~

Factory runs for real locally.

Hub routes the user to the right product/official extension.

Later Cloudiagram can produce the polished investor/client PPTX from a sanitized snapshot.

That is the program Claude should execute.
