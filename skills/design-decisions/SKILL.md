---
name: design-decisions
description: Makes and documents FRC robot design decisions before and during CAD — requirements from the game manual, architecture selection, KrayonCAD concepting, mechanism archetype trade-offs, materials, fasteners, 3D printing vs machining, controllability (backlash, hardstops, sensors), and weight/packaging budgets. Use for "which intake/elevator/arm should we use", "decision matrix", "what material/thickness/fastener", kickoff strategy-to-CAD, or any trade-off question.
---

# Design Decisions

FRCDesign.org is authoritative for design choices. Present decisions as: requirement → options → criteria → choice → consequences for the layout sketch.

## Process

1. **Requirements**: from the current game manual — frame perimeter, height/extension limits, bumper rules, weight limit, gamepiece geometry/material, field element positions, scoring targets. Never assume last season's rules; state which manual/year was used.
2. **Strategy → functions**: intake, index/hold, score (which targets), climb, drive. Rank by priority.
3. **Architecture options**: sketch 2–4 candidates in copies of a base layout studio (drivetrain + limits + field). Add **KrayonCAD** blocks (FRCDesignApp → insert, Configure, fasten/revolute to provided mate connectors) for 3D packaging.
4. **Decision matrix**: criteria weighted (cycle time, reliability, complexity/buildability, weight, packaging, control difficulty, team capability & tools, cost). Score, pick, record rationale in the layout sketch document/tab description.
5. **Prototype-driven numbers** (compression, roller spacing, wheel choice) feed the layout sketch.
6. Freeze architecture → proceed to `main-layout-sketch`.

## Archetype quick guide

- **Intake**: slapdown/pivot (fast deploy, fine position control, simple) vs 4-bar/linkage (stows horizontally, more parts) vs fixed. Golden rules: roller surface speed ≥ 2× robot speed; maximize grip and width; squishy piece → rigid rollers, hard piece → compliant; robust outside frame perimeter (polycarb/SRPP, not aluminum); use sensors.
- **Elevator**: cascade (stages move equally, COTS rigging, stronger intermediate stages, harder >3 stages) vs continuous (easy to add stages, inner moves first, less reduction, indeterminate stage positions).
- **Pivot/arm**: dead axle (structural, stronger) with chain + large sprocket bolted to arm; minimize backlash; keep mass low/central; torque = weight × CoG distance at worst angle.
- **Shooter**: flywheel diameter (4" common) and mass (recovery vs spin-up), compression, contact time/wrap, back rollers for spin control, fixed vs adjustable hood; avoid compliant/treaded flywheel wheels that expand at speed.
- **Drivetrain**: swerve (COTS module, e.g. MK4i: 1.75" tube-to-ground, 4.25" corner offset) with 2x1 1/8" wall outer rails; bellypan keeps rails parallel.

## Fast rules (details in references)

- Materials: 6061-T6 default; 1/16"/0.090" gussets & bellypans; 1/8" structural; 1/4" high-load pivots; 1/4" polycarb or SRPP outside frame; no wood on robot; no Loctite near polycarb (use 425 or Vibra-Tite VC-3). → `references/materials-fasteners.md`
- Fasteners: #10-32 everywhere, 1/4-20 for high strength, nylock default, 3/16" rivets + ≥1 bolt per joint, ~5 threads engagement when tapping. → `references/materials-fasteners.md`
- 3D printing: print when no COTS/faster/cheaper/unmachinable; load in XY; teardrop horizontal holes; metal inserts for hex bores; no printed pinions/drive gears. → `references/3d-printing.md`
- Controllability: mechanical hardstops everywhere possible; absolute encoders where no hardstop/backlash; fewer stages; belt-driven encoder off pivot. → `references/controllability.md`

## Output

A short decision record: chosen architecture, key numbers (ratios, extension, positions), open risks, and the list of layout sketch entities to add.
