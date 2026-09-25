---
name: assembly-setup
description: Builds fast, robust Onshape assemblies for FRC — Origin Cube group-and-fasten method, rigid subassemblies per moving body, motion mates between origin-cube mate connectors, Replicate for hardware, FRCDesignLib COTS, patterns, mirror, relations, folders, and top-level robot assembly. Use for "assemble", "mate", "add bolts/rivets", subsystem or robot assemblies, laggy assemblies, or making a mechanism move.
---

# Assembly Setup

> - **Tree:** `frc-cad-foundations` › Assemble › **assembly-setup**
> - **Go deeper:** `mechanism-playbooks`
> - **Next:** `cad-review`

Method from FRCDesign.org Assembly Best Practices; mate/tool behavior from Onshape Help.

## Rigid subassembly (per rigid body)

1. Part studio already has Origin Cube (first feature) and, for moving systems, mate connectors for each DOF (pivot axis, slider start) **owned by the Origin Cube**, placed on derived layout geometry.
2. Insert the part studio parts + Origin Cube (green check immediately, no mating). Exclude `zREF` / reference composites.
3. **Group** all parts from that part studio.
4. **Fasten** Origin Cube mate connector to the assembly origin.
5. Duplicate + fasten identical parts (one instance modeled in studio).
6. Insert COTS/hardware from FRCDesignLib (simplified models), mate once, then **Replicate** onto matching holes; name the replicate.
7. Folders: `Tubes`, `Plates`, `Shafts & Spacers`, `COTS`, `Hardware`, `Motors`.

Parts added later: insert with green check, edit the existing Group, add them → they stay where modeled.

## Moving subsystem (top-level subsystem assembly)

- Insert each rigid subassembly. Fasten the static one's Origin Cube to origin.
- Mate moving bodies using the shared origin-cube-owned mate connectors: **Revolute** (pivot), **Slider** (elevator stage/carriage), with **limits** from the layout's travel.
- Cascade elevator: sliders per stage + **Linear relation ratio 1** between them. Geared pivots: Gear relation if you want coupled motion.
- Result: only a handful of mates per subsystem (e.g. one revolute for a slapdown intake).

## Top-level robot assembly

Insert each subsystem top-level assembly (by version from other docs), fasten each Origin Cube to origin. Because all studios share the robot origin, nothing needs positioning. Hide origin cubes when done.

## Speed rules

- Minimize mates; prefer low-DOF mates (Fastened, Group) and avoid tangent/parallel/planar mates and unnecessary limits.
- Rigid subassemblies (fully constrained or locked) let the parent skip solving.
- Simplified COTS (swerve modules, motors, electronics) from FRCDesignLib; import each fastener size once then Replicate.
- Circular/linear assembly patterns for repeated modules (e.g. 4 swerve modules). Assembly Mirror with **Transform** strategy for symmetric parts (keeps BOM count, no new parts).
- Configurable COTS (gear/pulley tooth count, spacer length, rivet grip length) — change configuration instead of re-inserting.

## Hardware detail

- Model fasteners where it helps BOM/clearance; time-box it during build season.
- Bolt length: stack-up rounded up to next stock length; nylock nuts default.
- Rivets: 3/16" blind rivets; pick configuration grip length matching the stack (e.g. 1/16" wall + 3/32" gusset = 0.156"). Every riveted joint needs ≥1 bolt.
- Washers on polycarbonate.

## Verify

Drag moving bodies through their limits (no interference: Check Interference / Section view Shift+X); mass properties vs weight budget; instance folders tidy; no unmated floating parts; mates count reasonable.
