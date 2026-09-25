# Dead-Axle Pivot / Arm (FRCDesign 2B; 2910 & 6328 2023 examples)

## Calcs
- Torque = weight × CoG distance, worst case at horizontal/full extension (ReCalc Arm, AMB).
- Typical 30:1–200:1. ≤3 stages including sprocket stage. State every stage and verify the product.
- Dead axle stiffness: 1/2" hex < 3/4" < 7/8" tube < SplineXL < 2" tube. 3/4" or 7/8" tube pairs with 1.125" OD bushings fitting most COTS sprockets. Large cantilevered arms → 2"+.
- Bushings (low speed, high load) or X-contact bearings for large dead axles.

## Layout
Origin Cube, crossbar, pivot point, drive sprocket position, c-c line (long enough for inline tensioner), PD circles (`#SprocketPD_25`), motor circle, arm length line, swept-range construction circle, hardstop positions, all scoring/stow angles.

## Part studio order
1. Pivot mate connector owned by Origin Cube (on derived pivot point).
2. Crossbar tubes. 3. Pivot support plates (1/4" alu for high load). 4. Chain + gearbox hex via FS. 5. Dead-axle tube, spacers, washers. 6. Arm tubes with bolt access holes. 7. Large driven sprocket (e.g. 60T #25) bolted directly to arm via spacer plate — axle purely structural. 8. Names/materials, folders.

## Backlash control
Shim tape, clock sprockets, strong spacers/bolting, fewer stages, sector gear for precision, tensioner, both sides driven by a cross shaft to avoid twist, absolute encoder belt-driven from pivot or zombie axle.

## Assembly
Rigid `Base` + rigid `Arm` subassemblies; top-level Revolute between their origin-cube pivot connectors with limits = hardstops.
