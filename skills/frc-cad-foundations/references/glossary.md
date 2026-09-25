# Glossary (FRC + Onshape)

| Term | Meaning |
|---|---|
| Main layout sketch (MLS, "master sketch") | Part studio of sketches holding robot-level geometry: drivebase, bumpers, extension limits, field elements, motion paths, gamepiece path. Derived into every subsystem. |
| Origin Cube | FRC FeatureScript: 2" transparent cube + mate connector at origin; optional FRC constants/functions. First feature in every part studio. |
| Derive / Derived | Onshape feature that brings parts/sketches/mate connectors from another part studio (same or other document). One-way link. Version references need manual update (blue icon). |
| Composite part (open/closed) | Groups bodies as one unit. Closed = constituents not selectable; good for reference geometry. |
| Rigid subassembly | Subassembly with no internal DOF; parent skips solving it → fast. |
| Group mate | Locks instances at current relative positions (use for parts from one part studio). |
| Replicate | Copies a seed instance + its mate onto all matching geometry (e.g. every 0.196" hole). |
| c-c | Center-to-center distance. |
| PD | Pitch diameter. |
| DP | Diametral pitch (teeth per inch of pitch diameter). FRC gears usually 20 DP. |
| HTD 5mm | Standard FRC timing belt, 5 mm pitch; 9 mm or 15 mm wide. |
| #25 / #35 chain | 0.25" / 0.375" pitch roller chain. |
| Hex / Thunderhex | 1/2" or 3/8" hex shaft; Thunderhex = rounded hex (13.75 mm OD). |
| MAXSpline / SplineXL / SplineXS | REV / WCP spline shaft profiles. |
| Live axle / dead axle / zombie axle | Axle carries torque / is fixed & structural / spins with mechanism but carries little torque (for encoders or pass-through power). |
| Bellypan / brainpan | Electronics plate under / flipped over the drivebase. |
| Crush block | Insert inside thin-wall tube so bolts can be torqued without crushing. |
| Tube plug | Billet insert in tube end for gusset-less joints. |
| Nut strip | Tapped bar that replaces loose nuts behind polycarb/plate. |
| Crayon/KrayonCAD | Simplified, configurable subsystem blocks for fast architecture exploration (via FRCDesignApp). |
| FRCDesignLib / FRCDesignApp | Community COTS library / Onshape app to insert it. |
| OTB / UTB | Over- / under-the-bumper intake. |
| V4B / 4-bar | Virtual four-bar / four-bar linkage. |
| Hardstop / softstop | Mechanical travel limit / cushioned (or software) limit. |
| Regen / rebuild time | Time for Onshape to regenerate a part studio (see Feature list → Regeneration times). |
| Primitives | Rough measure of render complexity; fewer = less lag. |
| COTS | Commercial off-the-shelf. WCP, TTB, SDS, REV, AndyMark, CTRE are common vendors. |
