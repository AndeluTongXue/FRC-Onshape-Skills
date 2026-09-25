# Slapdown Intake (FRCDesign 2C; 4414-inspired) + linkage notes

## Golden rules
Roller surface speed ≥ 2× robot top speed; maximize grip (grippy material over extra compression); squishy piece → rigid rollers, hard piece → compliant; as wide as possible, center piece into frame; robust (lives outside frame); sensors.

## Design
- 1/4" polycarb main plates on 2x1 tube + nut strips; secondary plates aluminum.
- Rollers: dead-axle polycarb tube rollers with printed endcaps (configurable rollers) — dead axles double as rigid standoffs between arms. Keep 2 rollers on arm, third on fixed plate to lower pivot and stow height.
- Roller drive e.g. 1 Kraken @ 1.6:1.
- Pivot drive: one motor, planetary + chain to large arm sprockets; ~30:1–42:1 typical at the pivot (compute actual product). 1:1 belt to cross-axle, sprockets both sides (no twist). Inline chain tensioners. Zero at hardstop/ground → absolute encoder optional.
- Zombie axle: pivot axle carries roller power so roller motor stays on the base.

## Layout
Origin Cube, drivetrain + bumper profile, gamepiece path over bumper, rollers placed with belt c-c (reduced 0.02"), pivot point, deployed + stowed positions (in-sketch circular pattern), hardstops, frame perimeter/extension limit.

## Part studio order
Reference drivetrain front (closed composite) → superstructure tube (mirror; Assembly Mirror FS connectors) → derived nut strips → plates → shafts → arm + sprocket spacer → pivot mate connector owned by Origin Cube → belts/chain (teeth off) → names/materials.

## Assembly
Rigid `Intake Base` + rigid `Intake Arm`; top-level one Revolute with limits.

## 4-bar/linkage variant
Layout all four pivots + coupler in every state; each link its own rigid body; revolutes at pivots; verify no toggle/over-center within range. Stows more horizontally; more parts.
