---
name: main-layout-sketch
description: Creates and edits FRC main layout sketches ("master sketches") in Onshape — drivebase, bumpers, extension limits, field elements, mechanism motion paths, gamepiece path, and subsystem skeletons that drive all downstream parts. Use for "mastersketch", "layout sketch", "skeleton", robot geometry studies after kickoff, comparing architectures, or when any subsystem dimension should change.
---

# Main Layout Sketch (Mastersketch)

> - **Tree:** `frc-cad-foundations` › Layout › **main-layout-sketch**
> - **Also load:** `parametric-sketching`; `design-decisions` if the architecture isn't chosen yet
> - **Next:** Model branch: `parametric-sketching`, `part-studio-modeling`

Every downstream part should trace its critical dimensions back to here.

## What goes in

| Always | Sometimes | Never |
|---|---|---|
| Drivebase dims (frame perimeter, tube, module/wheel clearance) | Gear/pulley/sprocket pitch circles | Plate outlines, specific part shapes |
| Bumpers + starting configuration envelope + extension limits (from current game manual) | Belt / chain runs | Gussets |
| Field elements the robot interacts with | Motor locations | Mounting / bolt holes |
| End-effector / roller / wheel locations (from prototyping) | Pivot hardstop geometry | Fillets, pockets |
| Mechanism motion paths and all states (stowed, intake, score positions) | | |
| Gamepiece path (compression circles, tangents) | | |

Detail can be added later; start minimal.

## Build order

1. Part studio `Main Layout Sketch`: Origin Cube (first), then sketches.
2. **Drivetrain**: side view on Right plane, top view on Top plane (or on an auto mate connector of the side sketch). Make top-view size *equal* to side-view length so one dimension drives both.
3. **Bumpers, frame perimeter, height limit / extension limit boxes.** Rules change yearly — read the current game manual; never hard-code last year's numbers without saying so.
4. **Field elements** relevant to scoring/intaking, dimensioned from the field drawings relative to where the robot bumpers touch (hard alignment against bumpers reduces software/mechanical complexity).
5. **Each subsystem, one sketch each**, dimensioned from field elements, extension limits, or each other — every dimension must be intentional.
   - Pivots: pivot point, arm length line, construction circle of swept range; dimension neighbors a clearance distance from that circle.
   - Elevators: stage lengths driven by start/end manipulator positions from field targets.
   - Intakes: roller positions, gamepiece path over/under bumper, stowed vs deployed (circular-pattern the arm in-sketch to show stowed).
   - Shooters: flywheel circle, compression circle (e.g. 0.5" smaller radius), gamepiece circle, exit-angle line to target.
6. **Mate connectors** for every degree of freedom (pivot axis, slider start), owned by the Origin Cube (created in subsystem part studios on derived layout points).

## Organization

- One sketch per subsystem + per view; name like `MLS – Intake Side`, `MLS – Drive Top`.
- Color sketches per subsystem (sketch color property).
- Sketch all states of moving subsystems (separate sketches or configurations; configurations let you "animate").
- Fully define everything; use driven (reference) dimensions to read clearances without over-constraining.
- Folder: `Layout/`.

## Architecture comparison after kickoff

Build a base studio (drivetrain + extension limits + field elements), then copy it per candidate architecture and sketch each. Compare reach, cycle path, packaging, and clearance. Pair with KrayonCAD blocks for 3D volume checks (see `design-decisions`).

## Change procedure

1. Edit the dimension in the layout (never patch downstream parts to "make it fit").
2. Rebuild; confirm all sketches still black.
3. Version the concept doc; update derives in subsystem docs; fix any red features (see `cad-review`).

## Anti-patterns

- One giant sketch for the whole robot.
- Layout sketch containing plate outlines or holes (slows every derive and couples unrelated edits).
- Dimensions typed as magic numbers where a field element or limit exists to reference.
- Positioning subsystems in the assembly instead of the layout.
