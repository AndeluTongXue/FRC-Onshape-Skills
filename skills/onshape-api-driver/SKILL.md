---
name: onshape-api-driver
description: Drives Onshape programmatically (REST API and FeatureScript) or, as fallback, through the browser UI to execute FRC CAD tasks — URL/ID anatomy, auth, reading and adding features, sketches, variables, configurations, custom FeatureScript features, assemblies, versions, exports, and safe edit/verify loops. Use when an agent must actually create or modify Onshape geometry, call the Onshape API, write FeatureScript, or automate Onshape in a browser.
---

# Onshape API / UI Driver

Assumes `frc-cad-foundations`. Behavior per Onshape API docs (onshape-public.github.io/docs) and Help. Details in `references/api-cheatsheet.md`; UI shortcuts in `references/ui-shortcuts.md`.

## Principles

1. **Plan, then act.** Write the intended feature tree (names, references, parameters as expressions/variables) before calling anything.
2. **Template from reality.** The API omits defaults and JSON shapes are verbose. Build or find one instance of a feature by hand/in the doc, `GET` it, and use that JSON as the template. Same for custom FeatureScript `namespace` values.
3. **Expressions over numbers.** Send `"expression": "#frame_width/2"` or `"#BeltCTC_5mm(80,18,36)"`, not converted floats. Sketch geometry in the API is in **meters** — keep it minimal and let constraints/dimensions carry intent.
4. **Prefer high-level features** (Extrude Individual, Robot Shaft, Belt & Chain Gen, variables) over raw sketch entity generation. For complex repeated geometry, write a small custom FeatureScript rather than hundreds of API sketch entities.
5. **Write to workspaces only**; version before risky batches so you can restore.
6. **Verify every write**: check `featureState` (OK/ERROR/INACTIVE) in the response; re-GET features; run a FeatureScript eval to measure/count; check regen via rebuild timing. Stop and repair on the first ERROR — don't pile features onto a broken tree.
7. **Secrets**: API keys from environment variables only; never print them.

## Typical flows

**Add a variable, then a feature using it**
1. `GET /partstudios/d/{did}/w/{wid}/e/{eid}/features` → note existing IDs, rollback, serialization version.
2. `POST …/features` with a `variable` feature (template from GET), then the dependent feature referencing `#name`.
3. Confirm both `featureState: OK`.

**Change a driving dimension (flex test)**
Find the sketch/variable feature → `POST …/features/featureid/{fid}` with the edited expression → check all downstream featureStates → revert if the test was temporary.

**Insert & mate in an assembly**
`POST /assemblies/…/instances` (part studio or subassembly, by version for other docs, with configuration) → add `BTMMateConnector-66` / `BTMMate-64` features (FASTENED to origin via Origin Cube connector; REVOLUTE/SLIDER between origin-cube connectors) → GET definition to verify.

**Query geometry**: `POST /partstudios/…/featurescript` with a lambda (e.g. evaluate `qCreatedBy(makeId("Front"), EntityType.FACE)`, mass, bounding boxes, counts) to get deterministic IDs and measurements for verification.

**Export**: STEP/STL translation → poll translation → download blob.

## Browser UI fallback

- Use tool search Alt/⌥+C to find any feature by name (including custom FS).
- Read the feature list and parts list after every step; take a screenshot only when geometry must be inspected.
- Enter/confirm dialogs with the green check; Shift+Enter repeats the tool. Esc cancels.
- Don't rely on coordinates between steps — re-find elements each time.

## FeatureScript authoring (custom features)

- Feature Studio tab; `annotation { "Feature Type Name" : "…" } export const myFeature = defineFeature(function(context, id, definition) precondition { … } { … });`
- Keep features deterministic and fast; expose parameters with sensible bounds and units; reuse `opExtrude`, `opPattern`, `skSolve` sketches; add mate connectors via `opMateConnector` where assemblies need them.
- Version the Feature Studio document; users add via "Add custom features" and update via the blue icon / Update all.
