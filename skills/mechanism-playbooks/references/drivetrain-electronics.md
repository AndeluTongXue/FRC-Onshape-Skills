# Swerve Drivetrain + Electronics (FRCDesign 1D/1E, 2910 example)

## Layout
- Side view (Right plane): tube bottom 1.75" above ground (MK4i), wheel clearance box 4.625" wide (MK4i).
- Top view: square equal to side length (e.g. 26"×26" training default; use your frame size variable). Inner square 1" smaller → 2x1 rails. Module cutout lines 4.25" from edges (MK4i; other modules differ), circular pattern ×4. Cross tubes (2x2 or 2x1) e.g. 8" apart.
- Bumpers envelope, frame perimeter; fully defined.

## Part studio
1. Origin Cube → Derive layout.
2. Extrude Individual tubes (up-to layout); Tube Converter late: outer 2x1 1/8" wall ("centered on tube" OK for drive rails), inner 2x2 1/16".
3. Bellypan 1/8": sketch one corner cutout with 1" fillets, circular pattern ×4 in sketch, extrude; Fillet All Edges 0.25"; rivet/bolt holes 0.196" via linear+circular sketch patterns — one extrude cut.
4. Gussets 1/8": project one tube hole, pattern, mirror.
5. Battery holder, electronics holes (Electronics Mounting FS or MechSketch profiles).
6. Materials 6061; names; folders. Pocketing (Part Lighten, 0.15" ribs, 3/16" radius diamond at 45°) only after review — saves ~3–4 lb.

## Assembly
- Group + fasten origin cube; simplified MK4i from FRCDesignLib mated once, assembly circular pattern ×4.
- 3/16" rivets (grip 0.125–0.250") replicated; leave bolt holes for gusset bolts (#10-32 + nylock); mirror via origin cube mate connector.
- Expect ~37 lb for the course drivetrain.

## Battery & electronics
- Battery ~13 lb → lowest possible, on bellypan; cutout ~6.705"×7.225"; 1/8" holder on 3/8" spacers; 1" or 2" strap slot.
- Place: PDH/PDP, controller (roboRIO/SystemCore — check current season; roboRIO retired for 2027), VRM/PH, main breaker (accessible, near PDH & battery), IMU near center, RSL visible, radio per vendor guidance. Leave wiring space; coordinate with electrical.
- Mounting: PDH #10-32, roboRIO #4-40, breaker 1/4-20, Pigeon 2.0 #6-32, Canandgyro #8-32; VHB if hole accuracy is uncertain.
- Wire pass-throughs in rails with grommets.

## Bumpers
- Separate part studio/assembly; at least a swept block model. Rules change yearly — check current manual (older: 2.5" noodles on 5"×3/4" plywood; ~3/4" ground clearance, 1/4" gap to frame recommended).
