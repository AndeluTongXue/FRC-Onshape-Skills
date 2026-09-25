# Designing for Controllability (FRCDesign.org)

- **Backlash** sources: gear mesh gaps, hex/bore slop, chain stretch, stage count, mounting flex. Fixes: fewer stages (≤3), shim tape in bores (wrap over bore edge), clock sprocket notches, green 680 sparingly, rigid spacers/bolting, sector gear or rack for precision.
- **Transmission choice**: chain for high-torque pivots (maximize wrap, always tension: inline, turnbuckle, sliding gearbox); belts for low torque/high speed, elevators, small pivots (near-zero backlash); gears/10 DP pivot or rack & pinion for lowest backlash.
- **Reduction sizing**: use ReCalc — too much adds backlash & dangerous torque; too little is slow/inaccurate.
- **Hardstops**: mechanical hardstops wherever possible (use existing structure). Softstops (TPU/foam) cushion but less consistent. Hall effect + magnet for zeroing where mechanical impossible.
- **Encoders**: motor relative encoder insufficient with backlash/no hardstop → absolute encoder. Through-bore only on live axles. Options: off-axis at same ratio (slop errors), belt direct from pivot shaft (precise), zombie axle at pivot.
- CAD implications: model hardstop geometry in layout sketch; reserve encoder and sensor packaging; add mate limits matching hardstops.
