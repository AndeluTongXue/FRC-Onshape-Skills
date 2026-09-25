# frc-onshape-cad

Skills for agents doing FRC robot CAD in Onshape. They favor parametric, top-down models with fast regeneration and lean feature trees.

Sources:
- FRCDesign.org is followed for design decisions and methodology.
- Onshape Help and the Onshape Learning Center are followed for how features, the UI, and the API behave.

| Skill | Purpose |
|---|---|
| frc-cad-foundations | Core rules, priorities, and workflow. Load first. |
| robot-document-architecture | Concept, subsystem, and main robot documents; versions; derive and import links |
| main-layout-sketch | Master and layout sketches that drive the robot |
| parametric-sketching | Fully defined sketches, plate, gusset, and mount recipes |
| part-studio-modeling | Feature tree order, FeatureScripts, regeneration-time control |
| power-transmission-cad | Ratios, belts, chain, gears, shafts, bearings, tensioning |
| tolerances | Team gear/belt c-c rules and fit allowances for holes, bearings, spacers, prints |
| naming-and-folders | Team naming rules for sketches, extrudes, parts; feature-tree, assembly, and tab folders |
| onshape-feature-rules | What Onshape features can and can't do: sketches, dimensions, extrudes, patterns, mates |
| part-sourcing | Finding COTS parts, trustworthy dimensions, and CAD from vendors |
| hole-feature | Hole feature options, fastener sizes, and one Hole per stackup |
| assembly-setup | Origin Cube method, rigid subassemblies, motion mates, Replicate |
| design-decisions | Requirements, architecture choice, materials, fasteners, 3D printing, controllability |
| mechanism-playbooks | Drivetrain, shooter, pivot, intake, and elevator recipes, plus example documents |
| cad-review | Parametric, performance, and organization audit, plus reference repair |
| onshape-api-driver | Driving Onshape through the REST API, FeatureScript, or the browser UI |

API use needs the `ONSHAPE_ACCESS_KEY` and `ONSHAPE_SECRET_KEY` environment variables.

## Install

- **Claude (Cowork / desktop):** download `dist/frc-onshape-cad.plugin` and open it in a chat to install.
- **Claude Code:** `/plugin marketplace add AndeluTongXue/FRC-Onshape-Skills`, then `/plugin install frc-onshape-cad@frc-onshape-skills`.
- **Other agents:** use the folders under `skills/` directly (each has a `SKILL.md`), or unzip `dist/frc-onshape-cad.zip`.
