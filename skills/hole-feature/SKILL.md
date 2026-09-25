---
name: hole-feature
description: How to use the Onshape Hole feature for FRC parts — hole styles (simple, counterbore, countersink), types (clearance, tapped, drilled), fits, termination, placement on sketch points, #10-32 as the default size and when to use #4-40, #6-32, #8-32, 1/4-20 and larger, and minimizing hole features by cutting a whole stackup with one Hole after every part it passes through exists. Use whenever adding bolt, rivet, or tapped holes, choosing fastener sizes, or cleaning up many hole or cut features.
---

# Hole Feature

> - **Tree:** `frc-cad-foundations` › Model › `part-studio-modeling` › **hole-feature**
> - **Also load:** `parametric-sketching`, `onshape-feature-rules`
> - **Next:** back to `part-studio-modeling`

Onshape behavior is from Onshape Help. Items marked [verify] should be checked in the dialog before relying on them.

## The key rule: one Hole feature per stackup

**Don't add the Hole until every part the fastener passes through exists.** Then cut the whole stackup with a single Hole feature. Example: a plate, then a 2x1 tube, then a gusset on the other side. Stack order and how deep the hole goes are set by **Termination** and the parts **scope**.

1. **Model the parts first**, without their fastener holes:
   - plates
   - tubes (hole-free blocks, or before Tube Converter)
   - gussets
   - brackets
2. **Place the points once:** make one sketch (e.g. `Bolt Holes`) on the outer face or plane of the stack. Put a **sketch point** at every fastener location.
   - Dimension the points from tube edges or layout geometry.
   - Pattern and mirror the points in that sketch.
3. **Add one Hole feature:**
   - Pick all the points.
   - Set the start plane.
   - Set **Termination = Through**, or **Up to entity** / **Blind in last** when the stack ends in a blind or tapped part.
   - Set the scope to **all parts in the stack**.
4. **Add another Hole feature only when something really changes:**
   - a different size or fit
   - a different style (counterbore or countersink)
   - a different termination
   - a different direction

### Why

- **Fewer features and faster rebuilds:** one hole cuts three parts instead of three extrude cuts.
- **Holes always line up** through every part, because one set of points drives all of them.
- **Moving a bolt is one edit**, and every part follows.

### Anti-patterns

- Adding a Hole to each plate as you model it, then more Holes later for the tube and the gusset.
- Using `Use` to project holes from one part to cut matching holes in the next.
- A separate Hole feature for each bolt location of the same size.

## Hole dialog: what each option does

- **Style:**
  - **Simple:** a straight hole.
  - **Counterbore:** a recess for SHCS heads. Use it only where a head must sit flush, which is rare in FRC.
  - **Countersink:** for FHCS. Use it only for flush flat-head bolts, e.g. on a bellypan or sliding surfaces.
- **Standard / type** (ANSI for FRC):
  - **Clearance:** the bolt passes through. Pick size and **fit**: Close, Normal or Loose. **Team default: Close.** #10 close = 0.196", which is the FRC standard and also fits 3/16" rivets.
  - **Tapped:** threads go into this part. It uses the tap drill size (#10-32 = 0.159"). Set the tapped depth, and optionally show cosmetic threads.
  - **Drilled:** a specific drill size. Use it for rivet-only holes if not using #10 close, or odd sizes.
  - **Pipe thread / PEM:** rarely needed. PEM applies only to sheet with PEM hardware.
- **Placement:** sketch points, vertices, circle centers or mate connectors.
  - It doesn't take bare regions.
  - Prefer sketch points in a dedicated sketch.
- **Start:**
  - **Start from part:** the hole starts at the first face it meets.
  - **Start from sketch plane.**
  - **Start from a selected plane or mate connector.**
- **Termination:**
  - **Blind:** set depth.
  - **Blind in last:** passes through every part in the scope and ends blind in the last one [verify the tapped behavior in the last part].
  - **Up to next.**
  - **Up to entity.**
  - **Through:** all parts in the scope.
- **Scope / parts to cut:** limit this to the stack. Never let it cut unrelated parts behind the stack.

## Sizes: #10-32 is the default

| Size | Close-fit clearance | Tap drill | Use it for |
|---|---|---|---|
| **#10-32** | **0.196"** | 0.159" | **Almost everything.** Structure, motor mounting (CIM-class 2" bolt circle), gussets, bearing retention, swerve modules, most COTS, 3/16" rivets. Default whenever nothing below applies. |
| #4-40 | 0.116" | 0.089" | roboRIO mounting |
| #6-32 | 0.144" | 0.1065" | Pigeon 2.0, SB50 connectors |
| #8-32 | 0.1695" | 0.136" | VersaPlanetary, Canandgyro, some nut strips and sensors |
| 1/4-20 | 0.257" | 0.201" | High-load joints where #10 isn't enough (pivots, climber hooks), main breaker, tapped churro (hex-lite) shafts |
| 5/16-18 | 0.323" | 0.257" | Extra high strength, shoulder bolts |
| 3/8-16 | 0.386" | 0.3125" | Tapped hollow hex shaft ends |
| M3 / M4 | 3.15 mm / 4.2 mm | 2.5 mm / 3.3 mm | Metric COTS only: NEO 550 and UltraPlanetary (M3), 775pro (M4). Match the vendor drawing. |

- **Tap only when it pays off:**
  - there's no access behind the part (inside a closed tube)
  - you want one-handed assembly
  - the part is thick enough
- **Target thread engagement:** about 5 threads (material thickness × TPI).
- **Otherwise use a clearance hole and a nylock nut, or a nut strip.**

## When not to use the Hole feature

- **Bearing bores, motor boss holes (1.25" / 1.5"), shaft and cable passthroughs:** sketch circles and cut with one Remove extrude. That extrude can also cover the stack.
- **Tube hole patterns:** Tube Converter or the tube's own pattern handles them.
- **Horizontal holes in 3D-printed parts:** they need teardrop shapes, which the Hole feature can't make. Sketch them.
- **Heat-set insert holes:** use a simple hole at the insert vendor's diameter, or a sketch circle.

## Verify

- There is **one Hole feature per size, style and termination** combination in each stack, not one per part.
- The **scope** includes every part in the stack and nothing else.
- In a section view (Shift+X), holes line up through all parts, and tapped depth ends inside the right part.
- **Flex test:** move a sketch point. Every part's hole should move with it.
