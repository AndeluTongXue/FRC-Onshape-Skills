---
name: cad-review
description: Audits and repairs FRC Onshape CAD for parametric robustness, regeneration/load time, feature-count bloat, organization, broken references, and design-rule violations, producing a prioritized findings list. Use for "review my CAD", "why is this slow", "flex test", "fix broken/red features", before versioning or release, or as the final verification step of any CAD task.
---

# CAD Review

Assumes `frc-cad-foundations`. Run it after every task, and when asked to review.

## 1. Parametric robustness (highest priority)

- [ ] Every part studio: Origin Cube first, Derive of layout second.
- [ ] All sketches fully defined (black). No red/over-constrained. Driven dims only for reference.
- [ ] Critical dimensions trace to the layout sketch, variables, or FRC functions, not magic numbers.
- [ ] No references to fillet/chamfer edges, tube holes, or faces later split. Plates dimension from tube edges.
- [ ] Extrude ends use Up-to references where length should track layout.
- [ ] **Flex test**: change 2–3 driving values (frame size, pivot height, a tooth count, tube length) ±0.5–1". Rebuild must stay green and parts must follow. Revert after.
- [ ] Configurations/variables defined before use and named.

## 2. Regeneration & load time

- [ ] Feature list → Regeneration times: list top 5 features and ms. Flag anything dominating.
- [ ] Slow FS (Tube Converter, Gusset Generator, lighten) at the end; teeth off on belts/chains.
- [ ] Face/part/sketch patterns instead of feature patterns; Reapply off.
- [ ] One of each part in studio; no unused derives; derives from versions; chains ≤3.
- [ ] Simplified COTS; rigid subassemblies; few mates; fasteners replicated not individually inserted.
- [ ] Imprinting disabled on sketches over complex faces.

## 3. Feature economy

- [ ] Same-depth holes cut together; repeated geometry patterned in sketch; Extrude Individual for multiple tubes.
- [ ] No features that do nothing (zero-effect, suppressed leftovers, duplicate sketches).
- [ ] But: separate sketches per subsystem/intent kept; cosmetic fillets as features.

## 4. Organization

- [ ] Features, sketches, parts, tabs, instances, replicates named; folders in tree and assembly.
- [ ] Materials set on every part; `zREF` bodies excluded in assemblies.
- [ ] Versions named; references updated or deliberately pinned.

## 5. Design rules (FRCDesign.org)

Aluminum not used outside frame perimeter; polycarb has no Loctite; drivetrain rails 1/8" wall; every riveted joint has a bolt; rivet grip matches stack; shafts retained; ≤2 fixed bearings/shaft; chains tensioned; ≤3 reduction stages; hardstops present; electronics accessible; interference check clean through full motion; weight vs budget.

## Repairing broken references (Onshape)

1. Find red features (errors) and yellow-triangle (missing selections).
2. Fix the **earliest** broken feature first — downstream errors often cascade.
3. Edit the feature, reselect the missing reference using stable geometry. Or use Repair (Versions & history → view in repair) to see the last good state and Replace reference (one-to-one; not for mate connectors / in-context refs).
4. For derived sketches that changed, re-pick in the Derive feature, then rebuild.
5. Re-run the flex test.

## Output format

```
Summary: <1–2 lines>, regen: <ms total / top offender>
Critical (breaks parametrics): …
Performance: …
Feature economy: …
Organization: …
Design rules: …
Fixed in this pass: …
```
