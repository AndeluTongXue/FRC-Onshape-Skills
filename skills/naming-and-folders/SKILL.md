---
name: naming-and-folders
description: Team naming and folder conventions for FRC Onshape CAD — short, plain names for sketches, parts, and extrudes only (everything else keeps its default name), plus how to group features, assembly instances, and tabs into folders and what to call them. Use whenever creating or renaming sketches, extrudes, or parts, organizing a feature tree or assembly, or when asked to "clean up", "organize", or "name" CAD.
---

# Naming and Folders

Assumes `frc-cad-foundations`. Goal: a teammate can read the feature tree at a glance.

## What gets a name

| Name it | Leave default |
|---|---|
| **Sketches** | Fillets, chamfers, patterns, mirrors, booleans, planes |
| **Extrudes** (including Extrude Individual) | Mate connectors, FeatureScripts (Tube Converter, Robot Shaft, Belt & Chain Gen, lighten) |
| **Parts** | Mates, replicates, assembly patterns, instances |

Don't spend actions renaming anything in the right column.

## Name rules

1. **Short:** 1–3 words, about 20 characters or fewer. It must not get cut off in the feature list.
2. **Plain:** say what it is, not how it was made. Use Title Case.
3. **No subsystem prefix** inside a subsystem's part studio; the tab already says "Intake". Exception: main layout sketches, where the prefix *is* the content (`Intake Side`).
4. **Standard abbreviations:** `PT` (power transmission), `T` (teeth), `L`/`R` (left/right), `2x1`/`1x1` (tube size), `c-c`.
5. **No versions, dates, "final", "new", "copy", or numbers like "2"** unless there really are two distinct parts.
6. **One sketch, one extrude:** give both the same name (`Side Plate` sketch → `Side Plate` extrude). Onshape's icons already tell them apart.
7. **Cuts:** name the extrude after what it removes (`Bearing Holes`, `Motor Holes`, `Pockets`).

### Sketches

| Good | Bad |
|---|---|
| `Tube Layout` | `Sketch 4` |
| `Side Plate` | `side plate outline sketch for intake v2` |
| `PT 12:60 14:70` | `PT - 12:60 + 14:70 20DP gear reduction stage` (truncates) |
| `Bearing Holes` | `holes` |
| `Drive Top` / `Intake Side` (layout studio) | `MLS – Intake – Side View – Deployed` |

Put tooth counts in PT sketch names so the ratio is readable (`PT 12:36 HTD`, `PT 16:60 #25`).

### Extrudes

`Side Plate`, `Tubes`, `Crossbar`, `Bellypan`, `Bearing Holes`, `Standoffs`.

### Parts

- Name the physical thing: `Side Plate`, `Pivot Shaft`, `Front Rail`, `Bellypan`, `Motor Plate`, `Roller Tube`.
- Add `L`/`R` only when left and right really are different parts: `Side Plate L`. Mirror-identical parts share one name and get duplicated in the assembly.
- Add stock size only when it separates two similar parts: `Crossbar 2x1`, `Crossbar 1x1`.
- Reference-only bodies: `zREF Frame`, `zREF Modules`. They sort last and are easy to exclude.
- Parts made by FeatureScripts (shafts, spacers, belts) keep their generated names unless they are ambiguous.

## Feature-tree folders

- **Top level, in tree order:**

  ```
  Origin Cube, Derive      (loose at top; no folder)
  Layout                   local construction sketches, mate connectors
  Frame                    tubes, crossbars
  Plates                   plates, gussets, bellypan
  PT                       PD sketches, belts/chains, gears
  Shafts                   shafts, spacers, standoffs
  Hardware                 derived nut strips, clamps, inserts
  Finish                   Tube Converter, fillets, lightening (slow features last)
  ```

- Use only the folders you need. Folder names are one word where possible.
- **Studios with several moving bodies** (elevator stages, intake base/arm): folder by body first (`Base`, `Arm`, or `Stage 1`, `Carriage`), then by type inside. Never nest more than 2 levels.
- **Timing:** create the folder when you add its first feature, not at the end.

## Assembly instance folders

Use `Frame`, `Plates`, `Shafts`, `PT`, `Motors`, `COTS`, `Electronics`, `Hardware`, `Subassemblies`, and only the ones that apply. Put replicated hardware in `Hardware`.

## Tabs and tab folders

- **Part studio tab:** subsystem name, e.g. `Intake`. With multiple studios, name them by body: `Intake Base`, `Intake Arm`.
- **Rigid assemblies:** `Intake Base Asm`, `Intake Arm Asm`. **Top level:** `Intake Asm`. **Robot:** `Robot Asm`.
- **Layout studio:** `Main Layout Sketch`.
- **Tab folders:** one per subsystem (`Drivetrain`, `Intake`, `Shooter`).

## Verify

- No `Sketch N`, `Extrude N`, or `Part N` names remain.
- No name is truncated in the feature list.
- Every feature sits in a folder except Origin Cube and Derive.
