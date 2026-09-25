---
name: parametric-sketching
description: Rules and techniques for fully-defined, parametric Onshape sketches for FRC parts — constraints vs dimensions, construction geometry, Use/project, expressions and variables, plate/gusset/motor-mount outlines, pitch-circle layouts, imprinting. Use whenever creating or editing any sketch, fixing blue/red (under/over-constrained) sketches, or drawing plates, tubes, gussets, or mounts.
---

# Parametric Sketching

Assumes `frc-cad-foundations`. Tool behavior from Onshape Help; FRC technique from FRCDesign.org Stage 1A–1C.

## Core rules

1. **Blue is bad, black is done, red is broken.** Finish every sketch fully defined. Onshape converts a dimension that would over-constrain to *driven* (gray, reference-only) — use that deliberately for clearance readouts.
2. **Less is better.** Minimum dimensions; prefer constraints: coincident, equal, symmetric, parallel, perpendicular, tangent, concentric, midpoint, horizontal/vertical, pierce.
3. **Anchor to the origin / default planes / derived layout geometry.** Sketch on stable planes or mate-connector planes, not on faces that may be removed.
4. **Construction geometry (Q) carries intent**: centerlines, pitch circles, bolt circles, center rectangles for hole patterns, clearance circles.
5. **Mirror/pattern in the sketch** across construction lines or the origin — never draw both sides by hand.
6. **Expressions not numbers**: `(60/20)"`, `#PulleyPD_5mm(36)`, `#BeltCTC_5mm(80,18,36) - 0.015in`, `#frame_width/2`. Enable Show Expression so intent is visible.
7. **Dimension from edges, not holes.** Plate holes reference tube edges (or project one tube hole then linear-pattern at 0.5"), so tube hole-pattern changes don't break plates.
8. **Use (U) only stable geometry** (layout sketch entities, primary tube faces). Used edges break if the source changes type.
9. **Imprinting**: turn *off* "Disable imprinting" only when you need existing edges; default to disabled imprinting for plate sketches on complex faces (faster, single region to select).
10. **Hold Shift** to suppress auto-inference when a stray constraint would be wrong. Arcs often catch accidental horizontal/vertical constraints — delete them.
11. Only **functional fillets** in sketches (tangent plate outlines); cosmetic edge breaks come later as features.

## Recipes

**Box tube profile** — rectangle; standard 1x1, 2x1, 2x2; lengths in 0.5" increments when possible.

**Drivetrain frame (top view)** — square equal to side-view length; inner square offset 1" (2x1 rails); module cutouts (e.g. MK4i 4.25" offsets) drawn once, circular-patterned 4×. Only design dimensions remain visible.

**Plate outline ("string around the holes")**
1. Fully define power-transmission construction (pitch circles, c-c lines) and bearing/bolt/clearance holes first.
2. Centerpoint arc around each corner hole, one arc dimensioned 0.25" from its hole, rest *equal*.
3. Tangent lines connect arcs. No sharp corners.
4. Keep plate edge a set distance from pitch circles (e.g. 0.25" beyond largest PD).

**Motor mount (CIM-class)** — 2.5" (or 60 mm) construction circle, 1.25" (or 1.5" for 12T pulley pass-through) center boss hole, #10-32 clearance 0.196" holes on 2" bolt circle via circular pattern; model only the holes you'll use. Put motor holes on the c-c line (coincident to infinite line) when useful.

**Four-bolt pattern** — construction center-point rectangle with holes at corners → 2 dimensions total.

**Gusset** — project at most one hole per tube with Use, linear-pattern the rest, mirror other side. Don't use Gusset Generator FeatureScript (breaks, inflexible).

**Pitch-circle transmission layout** — construction circles at PD (`teeth/DP` for gears, `#PulleyPD_5mm(n)` for HTD, `#SprocketPD_25(n)` for #25), tangent for gears, c-c dimension from FRC functions for belts/chain.

**Angled tube** — Aligned rectangle, angle by dimension.

## Hole sizes (sketch values)

#10-32 clearance 0.196" (also 3/16" rivet); 1/4-20 clearance 0.257"; #10-32 tap 0.159"; bearing bore 1.125" (1/2" hex flanged, tune to shop); motor boss 1.25"/1.5". Full table: `design-decisions` → fasteners.

## Common mistakes to catch

Over-dimensioning; referencing tube holes; blue sketches; one sketch mixing layout and detail; hand-drawn symmetric sides; numbers where expressions belong; stray auto-constraints on arcs; sketching on faces of features likely to change.
