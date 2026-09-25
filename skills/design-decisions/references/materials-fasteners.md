# Materials & Fasteners (FRCDesign.org Design Handbook)

## Materials
- **Aluminum 6061-T6**: default structure. **7075**: higher load, COTS hex shafts and gears (check before machining).
- Sheet: 1/16" or 0.090" gussets/bellypans; 1/8" structural plates & gussets; 1/4" high-load (pivots).
- Tube: drivetrain outer rails 1/8" wall; superstructure 1/16" wall with crush blocks; 1x1/2x1/2x2.
- **Polycarbonate**: impact parts outside frame; 1/4" typical; 1/32–1/8" covers/panels. Check real thickness (6 mm vs 1/4" = 0.014" off). No Loctite (use 425 or Vibra-Tite VC-3). Bearing hats for bearings.
- **SRPP**: stiffer, more impact-resistant, lighter than PC; ~$250/sheet vs ~$80; laser cut preferred; tolerates Loctite.
- **Steel**: ballast/max strength only. **Wood**: prototypes only.
- Don't use aluminum for parts outside frame perimeter (intakes).

## Structure joints
- Tube plugs (for 1/8" wall; sleeve for thinner): 2–4 bolts OK; tight hole position tolerance from tube end.
- Crush blocks (esp. 1/16" wall): printed 4–6 walls, teardrop holes, flange at tube end; mid-tube use external 1/16" plate instead.
- Gussets 1/16" or 0.090"; 3–4 bolts per corner typical; ≥1 bolt per riveted attachment.

## Fastener table (tap / close fit / SHCS key)
| Size | Use | Tap | Close fit |
|---|---|---|---|
| #4-40 | roboRIO | #43 0.089" | #32 0.116" |
| #6-32 | SB50, Pigeon 2.0 | #36 0.1065" | #27 0.144" |
| #8-32 | VersaPlanetary, Canandgyro | #29 0.136" | #18 0.1695" |
| #10-32 | motors, MAXPlanetary, swerve, most COTS | #21 0.159" | #9 0.196" |
| 1/4-20 | high strength, churro tap, main breaker | #7 0.201" | F 0.257" |
| 5/16-18 | extra high strength, shoulder bolts | F 0.257" | P 0.323" |
| 3/8-16 | hollow hex tap | 5/16" | W 0.386" |
Metric: M3 (NEO 550), M4 (775pro), M5, M6 (PDP lug).

## Retention & joining
- Nylock nuts default; Loctite 243 blue standard; 680 green for bearings/magnets/anti-backlash; 222 purple small adjusted.
- Rivnut/PEM for threads in thin material; heat-set inserts in prints; nut strips behind polycarb.
- Tapping: target ~5 threads engaged (thickness × TPI); 1/8" wall #10-32 OK for bearing retention.
- Rivets 3/16" blind; grip length must match stack; multi-grip ~0.187–0.437".
- SHCS default head; BHCS low profile; FHCS flush (countersink); shoulder bolts as small axles.
- CAD: model fasteners (FRCDesignLib → Onshape Standard Content → McMaster), import once, Replicate.
