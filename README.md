# frc-onshape-cad

[![Add to Claude: download .plugin](https://img.shields.io/badge/Add_to_Claude-Download_.plugin-D97757?style=for-the-badge)](https://github.com/AndeluTongXue/FRC-Onshape-Skills/raw/main/dist/frc-onshape-cad.plugin)
[![Other agents: download .zip](https://img.shields.io/badge/Other_agents-Download_.zip-555555?style=for-the-badge)](https://github.com/AndeluTongXue/FRC-Onshape-Skills/raw/main/dist/frc-onshape-cad.zip)

Click **Add to Claude**, then open the downloaded file in a Claude chat (desktop app or Cowork) to install. For Claude Code, see [Install](#install).

Skills for agents doing FRC robot CAD in Onshape. They favor parametric, top-down models with fast regeneration and lean feature trees.

Sources:
- FRCDesign.org is followed for design decisions and methodology.
- Onshape Help and the Onshape Learning Center are followed for how features, the UI, and the API behave.

## Skill tree

The skills form a tree rooted at `frc-cad-foundations`. Each skill assumes the skills on its path from the root, and each one opens with a navigation block (Tree, Also load, Go deeper, Next). Every skill can still trigger on its own. Branch names group skills and aren't skills themselves.

```
frc-cad-foundations              core rules, priorities, workflow (load first)
├─ Plan
│  ├─ design-decisions             requirements, architecture, materials, fasteners, 3D printing, controllability
│  ├─ part-sourcing                finding COTS parts, trustworthy dimensions, and CAD from vendors
│  └─ robot-document-architecture  concept, subsystem, and robot documents; versions; derive and import links
│     └─ naming-and-folders        names for sketches, extrudes, parts; feature-tree, assembly, and tab folders
├─ Layout
│  └─ main-layout-sketch           master and layout sketches that drive the robot
├─ Model
│  ├─ parametric-sketching         fully defined sketches; plate, gusset, and mount recipes
│  │  └─ onshape-feature-rules     what sketches, dimensions, extrudes, patterns, and mates can do
│  └─ part-studio-modeling         feature tree order, FeatureScripts, regeneration-time control
│     ├─ hole-feature              Hole feature options, fastener sizes, one Hole per stackup
│     └─ power-transmission-cad    ratios, belts, chain, gears, shafts, bearings, tensioning
│        └─ tolerances             team gear/belt c-c rules; fits for holes, bearings, spacers, prints
├─ Assemble
│  └─ assembly-setup               Origin Cube method, rigid subassemblies, motion mates, Replicate
│     └─ mechanism-playbooks       drivetrain, shooter, pivot, intake, and elevator recipes
├─ Review
│  └─ cad-review                   parametric, performance, and organization audit; reference repair
└─ Execute
   └─ onshape-api-driver           REST API, FeatureScript, or browser UI
```

On disk every skill is still `skills/<name>/SKILL.md`; the tree lives in the skills' content.

API use needs the `ONSHAPE_ACCESS_KEY` and `ONSHAPE_SECRET_KEY` environment variables.

## Install

- **Claude (Cowork / desktop):** click **Add to Claude** above (or download `dist/frc-onshape-cad.plugin`) and open the file in a chat to install.
- **Claude Code:** run these two commands:

  ```
  /plugin marketplace add AndeluTongXue/FRC-Onshape-Skills
  ```
  ```
  /plugin install frc-onshape-cad@frc-onshape-skills
  ```

  To get updates later, run `/plugin marketplace update frc-onshape-skills`.
- **Other agents:** use the folders under `skills/` directly (each has a `SKILL.md`), or click **Download .zip** above and unzip it.
