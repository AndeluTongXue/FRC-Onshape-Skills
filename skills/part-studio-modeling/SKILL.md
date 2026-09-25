---
name: part-studio-modeling
description: Builds lean, parametric, fast-regenerating Onshape part studios for FRC subsystems — feature tree order, Origin Cube and Derive, extrude choices, tubes, plates, shafts, spacers, patterns, FeatureScripts, materials, naming, and regeneration-time control. Use when modeling parts, adding features, choosing FeatureScripts, or when a part studio is slow or messy.
---

# Part Studio Modeling

Assumes `frc-cad-foundations` and `parametric-sketching`.

## What belongs in the part studio

Only parts your team manufactures or modifies: plates, cut tubes, shafts cut to length, custom spacers, 3D prints, modified COTS. **One of each unique part** — duplicate in the assembly. Unmodified COTS → assembly (FRCDesignLib). Reference geometry (frame from drivetrain, simplified modules) may be derived as a **closed composite**, sparingly.

## Canonical feature tree

```
Origin Cube                       ← always first
Derive: Main Layout Sketch(es)     ← only the sketches this subsystem needs
[Variables]                       ← local variables used below
Layout/           (folder: local construction sketches, mate connectors owned by Origin Cube)
Structure/        (tube sketches → Extrude Individual)
Plates/           (plate sketch → extrude → holes)
Power Transmission/ (PD sketches, Belt & Chain Gen, Robot Shaft, Robot Spacer)
Hardware refs/    (derived nut strips, chain comb, cable clamp if modified)
Finishing/        (Tube Converter, cosmetic fillets, Part Lighten)  ← slow & fragile last
Properties/       (Set Materials / Set Properties)
```

## Feature choices (Onshape behavior + FRC preference)

- **Extrude**: set Result = **New** explicitly for separate parts (Onshape may default to Add and merge). Prefer **Up to face / Up to vertex** (to layout planes, mate connectors, reference plates) over Blind for lengths that should track the layout. Symmetric for parts centered on a plane. One extrude may take many regions of the same part.
- **Extrude Individual** (FS): many regions → separate parts in one feature. Standard for tubes from a top-view sketch.
- **Tube Converter** (FS): converts blocks to punched tube. Slow → place near the end; select non-touching rectangles; 1/16" wall general, 1/8" for drivetrain outer rails; "auto offset" generally, "centered on tube" only for drivetrain rails. For elevators, prefer manual Shell + hole sketch + linear pattern count `((#tube_len/inch)*2)-1` at 0.5" (CADSHARP Measure Value) — more robust when lengths change.
- **Hole** tool for fastener holes when you want clearance/tap semantics and callouts; sketch + one Remove extrude for many identical through-holes (fewer features).
- **Patterns**: sketch patterns first; if a feature must repeat, use **Face** pattern where valid (much faster than Feature pattern), Part pattern for identical bodies; leave **Reapply features** off.
- **Mirror**: mirror parts/features about the Right plane when the origin lies on the symmetry plane. For left/right plates that are identical, don't mirror — duplicate in assembly.
- **Robot Shaft / Robot Spacer** (FS): parametric shafts (hex, rounded hex, MAXSpline) and spacers generated in place with offsets (e.g. 1/16" end offset for bearing flange). Use FS spacers for in-house spacers, FRCDesignLib configurable spacers for COTS.
- **Belt & Chain Gen** (FS): belts/chains from PD circles; **teeth off**. See `power-transmission-cad`.
- **Part Lighten / Vent / CheeseIt** (FS): pocketing only after design review; typical 0.15" ribs, 0.26" tool on gearbox plates. Don't pocket clamping plates.
- **Fillet All Edges** (FS) / Fillet: late in tree; 3/16" common on printed parts; chamfer (not fillet) bed-contact edges of prints.
- **Derive** block motors (FRCDesignLib) with a unique Differentiation Variable each. Use block geometry, not full-detail derives.
- **Boolean subtract, keep tools** for pockets that match an insert (e.g. SplineXS adapter in a printed pulley).
- **Composite parts**: closed composite for reference bodies you won't pick sub-faces on.
- **Configurations**: for real variants (roller length, tooth count); keep configured features few. Checkbox config to suppress detail for lightweight mode.
- **Variables**: define before use; `#name` in any field; Measured variables to capture lengths (e.g. spacer length between plates).

## Regeneration-time control

1. Open Feature list → Regeneration times; find the top offenders.
2. Move slow/fragile features (Tube Converter, lighten, fillets, gussets FS) to the end or into a suppressible folder.
3. Replace feature patterns with face/part patterns or sketch patterns; turn off Reapply.
4. Remove duplicate identical parts; remove unused derives; derive from versions.
5. Belt/chain teeth off; block/simplified COTS only.
6. Disable imprinting on sketches over complex faces.
7. If a studio grows huge, split by rigid body (e.g. per elevator stage) into separate part studios in the same doc.

## Finishing checklist

- All parts named (`Intake Side Plate`, `Pivot Dead Axle`), material set (6061-T6, 7075 for hex, polycarbonate, PETG/PLA for prints), appearance for printed vs metal.
- Sketches/features named; folders used; no suppressed junk.
- Flex test: change the driving layout dimension → studio rebuilds cleanly.
- Reference-only bodies named `zREF …` (sort last) and excluded on insert.
