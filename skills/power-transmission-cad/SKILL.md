---
name: power-transmission-cad
description: Designs and models FRC power transmission parametrically in Onshape — gear, belt (HTD 5mm), chain (#25/#35) ratios and center distances with Origin Cube functions, Belt & Chain Gen, shafts, bearings, bushings, spacers, retention, tensioning, and backlash control. Use for gearboxes, reductions, rollers, flywheels, pivots, elevators drives, "what ratio", "c-c distance", or modeling belts/chains/shafts.
---

# Power Transmission CAD

Assumes `frc-cad-foundations` and `parametric-sketching`.

## Ratio design

- Ratio = driven:driving teeth; torque × ratio, speed ÷ ratio. Compute every ratio explicitly and show the math (don't trust quoted totals — e.g. 16:1 × 48:12 = 64:1).
- Size ratios with ReCalc (reca.lc: motors, arm, flywheel, belts, chains) or AMB calc; state inputs (motor, current limit, load, target time/speed).
- Typical: arms/pivots 30:1–200:1 (intakes ~30–42:1 at pivot); rollers ~1:1 to 1:2 upduction; flywheels ~1:1 (e.g. 4:3); roller surface speed ≥ 2× robot top speed.
- **Fewest stages** (≤3 including final chain/sprocket stage) — backlash compounds each stage.

## Element choice

| Need | Use |
|---|---|
| High torque, pivots | #25 chain with big driven sprocket bolted to arm, or 10 DP / sector gear for precision |
| Low torque, high speed, near-zero backlash | HTD 5mm belt (9 or 15 mm), pulleys ≥ 24T for flywheels, high wrap |
| Compact reduction / direction change | 20 DP gears (odd count keeps direction, even reverses); bevels for 90° |
| Very high torque, weight OK | #35 chain |
| Elevator | Belt or chain drive + rigging (see `mechanism-playbooks`) |

## Parametric modeling procedure

1. In a PD sketch (Layout/ or Power Transmission/ folder): construction circles
   - gears: `teeth/20` in (20 DP) — tangent circles, c-c = (PD1+PD2)/2
   - HTD: `#PulleyPD_5mm(n)`; #25: `#SprocketPD_25(n)`
2. Set c-c with Origin Cube functions: `#BeltCTC_5mm(beltTeeth, n1, n2)`, `#ChainCTC_25(links, n1, n2)`.
   - Belt pitch length must be a multiple of 5 mm; stocked sizes in 5T steps.
   - Chain: even link count (no half links).
   - Series belt runs: subtract 0.010–0.020" from belt c-c (efficiency/backlash trade; FRCDesign uses 0.015–0.02").
3. Run **Belt & Chain Gen** on the PD circles (mate connector sets belt centerline/offset from plate); read reported tooth count; replace any target c-c with the function call. **Teeth off.**
4. Shafts via **Robot Shaft** (profile, length Up-to reference plate, end offsets for bearing flanges, retention type), spacers via **Robot Spacer** or FRCDesignLib configurable spacer.
5. Pulleys/sprockets/gears: prefer COTS configurable parts in the assembly (change tooth count by configuration, no re-mate). Printed pulleys need metal hex/spline inserts.
6. Motors: FRCDesignLib block motors (derive) or simplified models; CIM-class = 2.5" OD, #10-32 on 2" bolt circle.

## Shafts, bearings, retention

- Hex 1/2" or 3/8" (flat-to-flat), 7075; rounded hex (Thunderhex 13.75 mm); MAXSpline/SplineXL for big torque; dead-axle tube 3/4" or 7/8" (1.125" OD bushings) up to 2"+ for large cantilevered arms. Steel only as swap-in, not a design baseline.
- Flanged bearings pressed in metal (1.125" bore for 1/2" hex, tune to shop); flanges face inward toward each other. ≤ 2 fixed bearings per shaft; keep pulleys near bearings; avoid cantilevers.
- Bearings in polycarb → bolted bearing hats. Bushings for low-speed high-load pivots.
- Retention: tapped shaft end + bolt + washer (best; #10-32 rounded hex, 1/4-20 churro, 3/8-16 hollow hex) > retaining rings > shaft collars (prototype). Always retain.
- Sliding fits: 0.005–0.010" clearance; less for torque parts, more for spacers.
- Gaps: 1/8" between moving parts and structure; don't space parts against a bearing outer race.

## Tensioning and backlash

- Always provide chain tension: inline tensioner (needs chain length), turnbuckle, slotted/rotating gearbox, or eccentric. Plan c-c long enough in the layout.
- Belts: exact c-c usually fine; tension where high torque.
- Backlash fixes: shim tape on hex bores, clock sprocket notches, rigid mounting, fewer stages, sector gears or belt-driven absolute encoder direct from pivot.

## Verify

Rebuild green; change a tooth count → c-c updates; interference check between pulleys/belts and structure; ratio and surface speed written in the feature/sketch name (e.g. `PT – 12:60 HTD 80T`).
