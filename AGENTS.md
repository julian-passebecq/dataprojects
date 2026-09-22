# AGENTS.md — Data Projects Constellation

This is the global registry for the data/BI/Fabric/Databricks portfolio.

## Authority
- This repo owns category, scope boundary, project ownership and portfolio status.
- Product repos own implementation truth.
- datapasscontrol is a detailed sub-registry, not a second global authority.

## Anti-sprawl
- Do not promote every helper, fork or donor into a product.
- Keep the six core products distinct.
- Reuse donor code before rewriting it.
- Keep current state separate from target state.
- Do not introduce MongoDB or another mutable status store unless Git-backed JSON is proven insufficient.
- Toolboxes/extensions belong in the tooling category unless explicitly promoted.
- Domain projects such as FOIL validate the stack; they are not automatically general products.

## Before work
1. Read registry/constellation.json.
2. Read the relevant product/tool/service entry.
3. Inspect the actual owning repo.
4. Update registry status only when scope or milestone materially changes.

Keep this registry architectural and managerial; do not dump detailed code inventories here.
