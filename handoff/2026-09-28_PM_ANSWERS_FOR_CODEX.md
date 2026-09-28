# 2026-09-28 — PM DataPass answers for the Codex tech lead

From **PM DataPass 1** (Claude Opus 5.5), after Julian's answers of 2026-09-28 evening. Read with `2026-09-28_CODEX_TECH_LEAD_MASTER_BRIEF.md`.

## Julian's decisions (2026-09-28)

1. **First V4 product: DataPass V4** (understand a real project: file roles, milestones, static lineage, findings, SQL then PySpark analyzers). Prototype Cloud and Factory come after; not in parallel.
2. **V4 starts now.** DataPass `1.1.0-rc.1` stays the working version; the remaining rc.1 ergonomics fixes land alongside V4, no separate 1.1.0 wait.
3. **Codex is the V4 tech lead.** Claude coders start on V4 architecture work only after Codex's first ADRs (at least: common-engine ownership/package boundaries, semantic IR versioning, analyzer plugin contract, `datapass.understanding` compatibility).
4. **Session structure (Claude Control):** one global PM for all apps (the only one asking Julian feature questions) + one light coordinator per active app; a sub-PM only when an app runs > ~3 coders at once.

## Current DataPass state (implementation truth, verify with git)

- `julian-passebecq/datapass-vscode` `main`, prerelease **v1.1.0-rc.1** (commit `d62ff62`), qa:ui 13 reached / 0 not reached / 4 not automatable.
- V3 shipped: tree lenses + right rail (#154), Home + `datapass.links` v1 (#153), **`datapass.understanding` v1 contract + validator** (#151, `.datapass/understanding/<repoKey>/<path>.json`, states ok/stale/orphan/invalid, sha256 after BOM strip + LF), **Hop view** with two-way code sync (#159), Airflow static DAG view (#158, never executes Python), Git badges on diagram + file history (#157), overlay palette/themes (#152), realistic ETL demo `examples/v3/etl-demo` (#156).
- Contract docs: `docs/PREPARING_A_PROJECT.md` §17, `docs/guide/12_DATAPASS_HOP.md`; product intent `handoff/V3_PRODUCT_VISION.md`; Julian's ideas `handoff/ROADMAP.md` ("Idées de Julian").
- `datapass-vscode-common` receives schemas/examples by `npm run sync:common` from datapass-vscode (sync-owned: avoid circular ownership when the Common Semantic Core lands there).

## What the PM needs from Codex first

The ADRs above plus the LOT 1–2 work packets (Common Semantic Core alpha; understanding v1 → IR adapter; deterministic SQL analyzer; first V4 file-understanding UX), in the work-packet template. Put them in this repository or `datapass-vscode-common` `plan/v4-semantic-engine-factory`, and tell Julian; the PM turns them into coding waves.
