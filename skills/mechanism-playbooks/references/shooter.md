# Flywheel Shooter (FRCDesign 2A, 1678 2022 example)

## Calcs
- Trajectory from exit angle + exit velocity (Desmos/ReCalc flywheel). Surface speed ∝ RPM × diameter; 4" common.
- Example: 2× Kraken X60, 4:3 belt reduction, 4" wheels + 2× 4" brass flywheels, ~3000 rpm target, >12 m/s projectile.
- MOI: more = faster recovery, slower spin-up.
- Wheels: stealth, Colson, solid rollers; avoid compliant/treaded (expand at speed).
- Compression: prototype; softer pieces need more. Longer wrap = consistency. Back rollers (counter-spin) control spin and add contact; PTFE tape on hood adds speed.
- Friction: shorten belt c-c 0.01–0.02"; ≤2 fixed bearings/shaft; pulleys near bearings; belt runs on one plate; pulleys >24T.

## Layout
Target (e.g. goal side view at its field distance), drivetrain/bumpers, height box; flywheel circle + compression circle (0.5" smaller radius); gamepiece circle tangent; hood wheels tangent spaced by belt c-c; exit-angle line to target normal to compression-to-last-wheel line; motors placed by belt c-c; feeder circles.

## Part studio
Origin Cube → Derive → reference cross tubes (closed composite) → main side plate (holes → standoffs → PT construction → outline), mirror → 1x1 brace → shafts/belts via FS → printed HTD pulleys with inserts → hood (polycarb, zip-tie holes) → camera/sensor mount → names/materials.
Rigidity: 1/4" polycarb side plates, standoffs doubling as guides/mounts, cross brace.

## Assembly
Single rigid assembly (0 DOF); exclude reference tubes. Adjustable hood → separate rigid hood subassembly + revolute (rack & pinion relation if geared).
