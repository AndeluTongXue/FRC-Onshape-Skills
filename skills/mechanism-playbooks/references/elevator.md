# Elevator (FRCDesign 2D cascade)

## Choose
- Cascade: each stage moves equally relative to parent; COTS rigging; higher CoM mid-travel; intermediate stages stronger (good for climbing); hard beyond 3 stages.
- Continuous: easy to add stages; inner stage moves first; less reduction; indeterminate stage positions.

## Components
- Bearing blocks: WCP inline / inline clamping (TTB alternatives) or plate-built.
- Rigging drives design (motor mount, crossmembers). Cable clamp on crossmember (TTB: plate 1 to tube, plate 2 to plate 1; WCP bolts through both). Crush blocks where bolting through tube.
- Cable ends: ≥1 loop per stage; ratchet tensioner (WCP ratchet plate / cut ratcheting wrench on drilled hex spool); self-tightening knot; loosen clamp before tensioning.
- Drive: vertical chain bolted to first stage via chain comb; NEOs on MAXPlanetary (keep accessible).
- Hall effect + magnet for zero; upper mechanical stop.

## Layout
Extended side view first (from target heights & extension limit): 2x2 stage rectangles, stage/carriage bottom tubes; optional retracted view constrained to extended; front view with tube widths & spacing. Per-stage sketches with configurations to animate.

## Part studio order
1 Origin Cube + derive → 2 Extrude Individual tubes (no duplicates) → 3 tube conversion via Shell + parametric hole pattern (count `((#len/inch)*2)-1`, 0.5" pitch) rather than Tube Converter → 4 Transform/copy tubes → 5 crush blocks → 6 rope sweep (3 mm circle) → 7 chain comb derive → 8 chain + crossmember sketch with bearing holes → 9 crossmember plates/tube → 10 cable clamp derive + holes + crush block → 11 tube plug holes → 12 chain, spacers, axles → 13 MAXPlanetary mount derive → 14 bottom plates → 15 carriage nut strips, ratchet plate, rigging shaft → 16 reference mate connector mid base tube, owned by Origin Cube.
Hand-off point for teammates: after step 4.

## Assembly
Rigid `Base`, `Stage 1`, `Carriage`; top-level Slider mates with limits + Linear relation ratio 1 (cascade). Rotate mounting 90° for pass-through.
