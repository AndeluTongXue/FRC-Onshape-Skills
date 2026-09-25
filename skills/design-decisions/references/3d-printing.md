# Design for 3D Printing (FRCDesign.org)

- Print when: no COTS, faster/cheaper than machining, unmachinable geometry, iteration (camera/sensor mounts, compression tuning), metal strength not needed.
- FDM parts are weakest in Z → orient so loads are in XY.
- Tolerance adder start 0.004–0.020" by fit; sliding on axle 0.005–0.010"; calibrate per printer/material with test prints (holes print undersize).
- Horizontal holes: teardrop, 100° at top — no supports.
- Minimize overhangs; chamfer (not fillet) bed edges.
- Walls/infill: power transmission parts high infill (up to 100%); crush blocks 4–6 walls.
- Hex bores under torque (esp. Thunderhex) → metal inserts (ThriftyBot/WCP hex, SplineXS adapter; Thrifty Insert FS).
- Printed gears: OK for claws/secondary; not pinions or drive gears; wider face, lower DP for strength.
- Materials: PLA prototypes; PETG functional default; TPU impact/flex (bumpers of mounts, softstops); nylon/CF-nylon, PC, PA12-CF for strength. Dry filament.
- Export STEP when possible; STL has no units.
- CAD: use 3D Printed Mass FS for accurate mass; heat-set insert holes per insert vendor.
