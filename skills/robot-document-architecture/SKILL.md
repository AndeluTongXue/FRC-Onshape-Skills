---
name: robot-document-architecture
description: Sets up or audits the Onshape document structure for an FRC robot — concept/layout document, per-subsystem documents, main robot document, tabs, folders, Variable Studio, versions, derive/import links. Use when starting a new robot or subsystem, "set up the CAD", "organize the document", splitting a slow document, or fixing out-of-date linked references.
---

# Robot Document Architecture

Assumes `frc-cad-foundations`. Structure follows FRCDesign.org Best Practices; Onshape behaviors follow Onshape Help.

## Standard structure

```
Concept doc ──(Derive MLS)──▶ Subsystem docs (Drivetrain, Intake, Shooter, Elevator, …)
                                   │ (Insert top-level subsystem assembly, by version)
Main Robot doc ◀───────────────────┘
```

- **Concept document**: `Main Layout Sketch` part studio (+ KrayonCAD concept assembly). Optionally a Variable Studio with robot-wide values.
- **Subsystem documents** (one per mechanism, own version history): part studio(s) → rigid subassemblies → top-level subsystem assembly.
- **Main Robot document**: top-level robot assembly inserting each subsystem's top-level assembly. May be merged with the concept document (acceptable; creates a loop but one fewer doc).
- Small projects/training: everything in one document with folders (`Drivetrain/`, `Intake/`) is fine; split when load time suffers or >~100 tabs.

## Inside a subsystem document

- Tab order: part studio(s) first, then rigid subassemblies, then the top-level subsystem assembly.
- **0-DOF subsystem** (fixed shooter): 1 part studio + 1 rigid assembly.
- **Multi-DOF subsystem** (pivot intake, elevator): 1 part studio + one rigid assembly per moving body (e.g. `Intake Base`, `Intake Arm`; or `Elevator Base`, `Stage 1`, `Carriage`) + top-level assembly with only the motion mates.
- Optional team numbering, e.g. `0200-A Intake`, `0210-A Intake Base`, `0210-PS`, `0220-A Intake Arm`.

## Linking rules (Onshape behavior)

- Cross-document Derive/Insert references a **version**. Create a version in the source (named, e.g. `v1.3 – intake pivot moved 0.5"`) before linking; update consumers deliberately (blue icon = newer version available → Update / Reference manager). Pin references that must not move.
- Same-document references may track the workspace (live). Live is convenient but regenerates more; prefer version references for large or frequently changing sources.
- Keep derive chains short (≤ ~3 levels). Never create circular references.
- Only derive what you need: the relevant layout sketches, maybe the frame as a closed composite for reference. Don't derive full COTS or whole robots into part studios.

## Variables

- Robot-wide numbers (frame length/width, bumper thickness, tube size, wheel diameter, extension limit) belong in the layout sketch dimensions or a **Variable Studio** (checkbox "available in all studios"; cross-document via Insert Variable Studio, needs a version).
- Feature-local numbers stay local. Don't create a variable for a value used once.

## Setup procedure (new robot)

1. Create `<Team> <Year> Concept` with part studio `Main Layout Sketch` (Origin Cube first). Build layout (see `main-layout-sketch`). Version it.
2. For each subsystem: create `<Team> <Year> <Subsystem>`; part studio starts with Origin Cube → Derive layout sketches (from the version). Build parts, subassemblies, top-level assembly. Version it.
3. Create/choose Main Robot doc; insert each top-level subsystem assembly (by version); fasten each Origin Cube to the origin (see `assembly-setup`).
4. Tab manager: folders per subsystem, consistent names.
5. Iteration loop: change layout → version concept → update derive in affected subsystems → fix → version subsystems → update main robot.

## Audit checklist

- Every part studio: Origin Cube first, derive second.
- No subsystem modeled in the main robot document.
- References up to date or intentionally pinned; no broken (red) derives.
- Versions named meaningfully.
