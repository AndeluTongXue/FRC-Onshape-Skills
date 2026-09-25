---
name: mechanism-playbooks
description: Step-by-step parametric Onshape build recipes for common FRC mechanisms — swerve drivetrain with bellypan/electronics/battery/bumpers, flywheel shooter, dead-axle pivot/arm, slapdown intake, cascade elevator — including their layout sketches, part studio feature order, and assembly structure. Use when asked to CAD a drivetrain, shooter, arm, pivot, intake, elevator, or electronics layout, or to find reference robot CAD.
---

# Mechanism Playbooks

Assumes `frc-cad-foundations`; uses `main-layout-sketch`, `part-studio-modeling`, `power-transmission-cad`, `assembly-setup`. Numbers are FRCDesign.org course defaults — adapt to the current game and prototypes.

Every playbook follows the same skeleton:

1. **Requirements & calcs** (ReCalc/AMB) → write key numbers into variables or layout dims.
2. **Layout sketch** entries in the Main Layout Sketch studio.
3. **Part studio** feature order (Origin Cube → Derive → …).
4. **Assembly**: rigid subassembly per rigid body → top-level with motion mates + limits.
5. **Flex test** the driving dimension, check regen time and interference.

Pick the reference file:

| Mechanism | File |
|---|---|
| Swerve drivetrain, bellypan, battery, electronics, bumpers | `references/drivetrain-electronics.md` |
| Flywheel shooter | `references/shooter.md` |
| Dead-axle pivot / arm | `references/pivot-arm.md` |
| Slapdown (and 4-bar) intake | `references/intake.md` |
| Cascade / continuous elevator | `references/elevator.md` |
| Public example Onshape documents | `references/example-documents.md` |

When the user wants a mechanism not listed (climber, turret, indexer, telescope), compose from these: pivots → turret/wrist; elevator → telescope/climber; intake rollers → indexer. Keep the same skeleton.
