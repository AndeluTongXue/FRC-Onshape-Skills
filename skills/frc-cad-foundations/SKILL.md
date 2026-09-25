---
name: frc-cad-foundations
description: Core doctrine for any FRC robot CAD work in Onshape — parametric top-down design, low regeneration time, lean feature trees, origin conventions, naming, and source precedence. Load this first whenever asked to "CAD", "model", "design", "build in Onshape", or edit any FRC robot, mechanism, part studio, or assembly; the other frc-onshape-cad skills assume it.
---

# FRC CAD Foundations (read before any other FRC Onshape skill)

This skill sets the non-negotiable rules. Task-specific skills (layout sketch, sketching, part studio, assembly, power transmission, design decisions, mechanism playbooks, review, API) build on it.

## Priority order when rules conflict

1. **Parametric design intent** — geometry must update correctly when a driving dimension changes.
2. **Low regeneration time / load time** — rebuild speed of part studios and solve speed of assemblies.
3. **Minimal features** — the fewest features that still express clear design intent. Never merge unrelated intent into one feature just to cut the count; never add features that a sketch constraint, pattern, or variable could replace.
4. **Readability** — named, foldered, ordered so a teammate can edit it.

## Source precedence

- **Design decisions** (what to build, materials, ratios, architecture, hardware, document/assembly structure): FRCDesign.org wins.
- **What an Onshape feature does and how the UI/API behaves**: Onshape Help / Onshape Learning Center (OLC) wins.
- If still ambiguous, choose the option that is more parametric and lighter to regenerate, and state the assumption.

## The ten rules

1. **Top-down always.** Robot geometry lives in a *main layout sketch* part studio. Every subsystem part studio starts by deriving it. Parts are modeled on top of layout geometry, never positioned by eye. (See `main-layout-sketch`.)
2. **One robot origin.** Origin = center of the drivebase, at floor level. Same origin in every part studio and assembly (also matches robot code / AdvantageScope).
3. **Origin Cube is the first feature** of every part studio (FRC Origin Cube FeatureScript). It anchors assembly mating and exposes FRC functions (`#PulleyPD_5mm`, `#BeltCTC_5mm`, `#SprocketPD_25`, `#ChainCTC_25`, bolt-hole constants).
4. **Fully define every sketch** (black, not blue). "Less is better": fewest dimensions; use constraints, symmetry, equal, patterns, `Use` projections of *stable* layout geometry.
5. **Drive with values, not copies.** Put shared dimensions in variables (`#frame_width`) or layout sketches; type expressions (`(60/20)"`, `#BeltCTC_5mm(80,18,36)`) instead of computed numbers.
6. **Reference stable geometry only**: origin, default planes, layout sketch entities, mate connectors, tube *edges* (not tube holes), variables. Never reference fillet/chamfer edges or faces a later feature can split.
7. **Model each manufactured part once** in the part studio; duplicate in the assembly. Unmodified COTS goes straight into the assembly from FRCDesignLib, not the part studio.
8. **Keep it light**: simplified COTS models, block motors, belt/chain teeth off, slow FeatureScripts (Tube Converter) near the end of the tree, face patterns over feature patterns, rigid subassemblies, few mates, Replicate for hardware.
9. **Name and folder as you go**: sketches, features, parts, tabs, instances, replicates. Set material on every part.
10. **Verify after every change**: rebuild is green, sketches black, flex a driving dimension, check regen times, check interference. (See `cad-review`.)

## Feature-count discipline (the "to a certain extent" rule)

Do reduce features by:
- extruding many regions in one feature (Extrude Individual for separate parts; one extrude for same-part regions),
- patterning/mirroring in the sketch rather than re-drawing,
- cutting all same-depth holes in one extrude or Hole feature,
- using one feature pattern/mirror instead of repeating features.

Do NOT reduce features by:
- cramming multiple subsystems' geometry into one sketch (layout sketches are one per subsystem),
- skipping construction geometry that carries intent,
- putting cosmetic fillets inside profile sketches (OLC: only functional fillets in sketches; edge breaks as late features),
- merging features whose inputs change independently.

## How to act in Onshape

- **Primary**: tool-agnostic methodology. Decide the design, the tree, and the parameters first; then execute through whatever interface exists.
- **REST API / FeatureScript**: load `onshape-api-driver`.
- **Browser UI** (e.g. Claude in Chrome): use Onshape shortcuts (Alt/⌥+C tool search, Shift+E extrude, U use, Q construction, D dimension, I insert, M fasten). Read the page/feature list after each step to confirm state; don't assume a click worked.

## Workflow for any CAD request

1. Clarify the requirement (game task, envelope, gamepiece, targets). If designing, load `design-decisions`.
2. Locate/confirm the document structure (`robot-document-architecture`).
3. Update or create the layout sketch (`main-layout-sketch`).
4. Model parts (`parametric-sketching`, `part-studio-modeling`, `power-transmission-cad`).
5. Assemble (`assembly-setup`).
6. Review (`cad-review`) and report: what changed, which driving parameters exist, regen time, open issues.

Reference: `references/glossary.md` for FRC/Onshape terms.
