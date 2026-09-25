---
name: tolerances
description: Team tolerance standards for FRC Onshape CAD — gear pitch circles +0.005" in diameter and constrained tangent (c-c = nominal + 0.005", no c-c dimension), belt center-to-center (-0.005"), plus bearing, shaft, spacer, hole, and 3D-print fit allowances. Use whenever sketching gear meshes, belt or chain runs, bearing bores, shaft/spacer fits, clearance or tapped holes, printed parts, or when asked about tolerances, fits, clearances, or "how much gap".
---

# Tolerances

Assumes `frc-cad-foundations`, `parametric-sketching`, and `power-transmission-cad`. **The team rules in this skill override the c-c adjustments in FRCDesign.org and in the other skills.** Build every tolerance into an expression so the nominal value is still visible.

## Team rules (mandatory)

### Gears: each pitch-circle diameter + 0.005"

- **Don't dimension between the gear circles.** Draw each gear's pitch circle **0.005" larger in diameter**, then constrain the two circles **tangent**.
  - Two meshing gears add 0.010" of diameter in total.
  - Because c-c = (D1 + D2)/2 for tangent circles, the modeled c-c ends up **nominal + 0.005"**.
  - Keeping tangency (instead of a c-c dimension) means the mesh still follows tooth-count changes without re-dimensioning.
- **Diameter expression (20 DP):** `(teeth/20)" + 0.005"`.
  - Example: 12T is `(12/20)" + 0.005"`, and 60T is `(60/20)" + 0.005"`.
  - Nominal c-c is (0.6 + 3.0)/2 = 1.800". Modeled c-c is (0.605 + 3.005)/2 = 1.805".
- Name the circles so the intent is clear, e.g. `PD 12T +0.005D`.
- **Idler chains and gear trains:** give every gear in the train the enlarged circle and chain the tangent constraints. Each mesh then sits 0.005" farther apart than nominal.
- **Gear shafts are then located by the tangency, not by a dimension.** Constrain the other degrees of freedom instead: the angle of the c-c line, and one shaft's position.
- **Don't** add this tolerance again anywhere else, such as a dimension, variable or mate offset.

### Belts: c-c = nominal − 0.005"

- **Dimension the belt c-c** with the Origin Cube function minus 0.005":
  - `#BeltCTC_5mm(beltTeeth, n1, n2) - 0.005in`
  - Example: `#BeltCTC_5mm(80, 18, 36) - 0.005in`
- **Pulley circles stay nominal:** `#PulleyPD_5mm(n)`. The tolerance goes in the c-c dimension, not the circles.
- **Series belt runs:** apply −0.005" to **each** belt's c-c.
- This replaces the FRCDesign.org guidance of −0.010" to −0.020".

### Chain

The team hasn't set a chain rule. Use nominal `#ChainCTC_25(links, n1, n2)` and provide tensioning (see `power-transmission-cad`). Ask the user before inventing a chain offset.

## Default fit allowances (FRCDesign.org; tune per shop and printer)

| Feature | Value |
|---|---|
| #10-32 clearance (also 3/16" rivet) | 0.196" |
| #10-32 tap | 0.159" |
| 1/4-20 clearance / tap | 0.257" / 0.201" |
| 1/2" hex flanged bearing bore | 1.125" nominal. Press fit in metal; adjust for machine or router. |
| Parts sliding on an axle (custom or printed) | +0.005" to +0.010" clearance |
| Torque-transmitting bores (pulleys, gears) | Toward 0.005". Keep tight. |
| Spacers | Toward 0.010". Looser is OK. |
| Spacer-to-tube gap | 0.010" |
| Moving part to structure gap | 1/8" |
| 3D-print "tolerance adder" | 0.004"–0.020" depending on fit. Calibrate with test prints; holes print undersize. |
| Horizontal printed holes | Teardrop, 100° at top |
| Stock thickness | Model the real stock thickness (e.g. 6 mm "1/4"" polycarb is 0.236", not 0.250"). |
| Oversize holes for clamping (e.g. Mitee-bite) | +0.005" |

## How to apply

1. Before adding any power-transmission sketch, decide the element type and apply the matching team rule above.
2. **Keep tolerances in expressions**, not typed numbers.
   - Good: `(48/20)" + 0.005"`
   - Bad: `2.405"`
   - If several parts share a tolerance, put it in a variable, e.g. `#gear_tol = 0.005 in` (diameter), `#belt_tol = 0.005 in`. Then gear diameters are `(n/20)" + #gear_tol` and belt c-c is `#BeltCTC_5mm(...) - #belt_tol`. One edit then updates the whole robot.
3. **Belt & Chain Gen:** run it on the nominal pulley circles. The c-c dimension already carries the −0.005".
4. **Verify:**
   - Measure the gear c-c. It should read nominal + 0.005", and there should be no driving dimension between the gear centers.
   - Measure the belt c-c. It should read nominal − 0.005".
   - Change one tooth count. Both rules must still hold after the rebuild.

## Review flags (for `cad-review`)

- Gear c-c set by a driving dimension, or gear circles at exact nominal PD.
- Belt c-c at exact nominal, or using an FRCDesign −0.015" / −0.02" offset instead of −0.005".
- Tolerance typed as a computed number instead of an expression.
- The same tolerance applied twice (enlarged circles *and* an offset dimension).
