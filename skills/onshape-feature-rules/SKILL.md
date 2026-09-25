---
name: onshape-feature-rules
description: What Onshape can and cannot do, so the agent plans valid operations — what sketch entities can be dimensioned or constrained to each other, what can be sketched on, what regions can be extruded and how extrude results split or merge parts, and the limits of revolve, sweep, patterns, mirror, holes, derive, composites, mate connectors, mates, configurations, and imported geometry. Use before any sketch, dimension, extrude, or feature choice, when a feature errors or goes red, or when asked "can Onshape…".
---

# Onshape Feature Rules (Can / Can't)

> - **Tree:** `frc-cad-foundations` › Model › `parametric-sketching` › **onshape-feature-rules**
> - **Next:** back to the sketch or feature you were planning

Source: Onshape Help / OLC. Items marked [verify] come from partial docs or memory; confirm in the UI or with a test before building on them.

## Sketch planes

| Can sketch on | Can't sketch on |
|---|---|
| Default planes (Top, Front, Right); Plane features | Curved or cylindrical faces |
| Planar faces of parts | Edges, points or axes alone (make a Plane or mate connector first) |
| Mate connectors (explicit, or implicit ones inferred while picking the plane), using their XY plane | |

- **Prefer planes and mate connectors over part faces.** A face can change or disappear, and imprinting on complex faces slows the sketch. Use "Disable imprinting" when you don't need the face edges.

## Dimensions and constraints

**Can dimension:**
- **Point ↔ point:** linear distance. Where you drop the dimension decides horizontal, vertical or aligned.
- **Point ↔ line:** perpendicular distance.
- **Line ↔ line, parallel:** distance.
- **Line ↔ line, not parallel:** angle. Where you place it picks the quadrant.
- **Circle/arc:** diameter or radius. Arc length is also available.
- **Circle ↔ point, line or circle:** measured from the **center** by default. Onshape can also dimension to the circle's edge (min/max, "tangent to arc") [verify how the option is chosen in the UI].
- **To external geometry:** origin, default planes, other sketches' entities, and part edges or vertices. They are referenced (projected) onto the sketch plane.
- **Value types:** expressions with units and functions (`+ − * /`, parentheses, `sqrt`, `sin`, `cos`, `tan`, `min`, `max`, `abs`, `floor`, `ceil`, `round` [verify list]), Origin Cube functions (`#BeltCTC_5mm(...)`), and mixed units (`1in + 5mm`).
- **Negative values** flip the direction for distances and angles, but not for radius or diameter.

**Can't / avoid:**
- **At least one end must be geometry in the current sketch.** You can't dimension between two external entities.
- **No over-defining.** An extra dimension on a fully constrained entity becomes **driven** (gray, reference only), or the sketch goes red. Remove the conflict; don't pile on dimensions.
- **Don't dimension what a constraint expresses.** Use equal, symmetric, tangent, coincident or midpoint instead of a number.
- **Gear meshes:** no c-c dimension between pitch circles. Use tangency (team rule, `tolerances`).
- **An angle needs two lines.** To angle-dimension from points, draw a construction line through them first.
- **Dimensions can't reference features below the sketch** in the feature tree (rollback order). Reorder or reference upstream geometry.
- **Use (U) projections** follow their source but break if the source changes type, e.g. a circle becomes a line.

**Constraint rules:**
- Tangent, concentric and equal need compatible entities: curves, circles and arcs, or like-for-like.
- **Pierce** ties a sketch point to a curve that leaves the sketch plane (sweep paths).
- **Fix** is a last resort. Anchor to the origin or planes instead.

## Regions and extrude

**Can extrude:**
- Closed sketch regions. Overlapping closed curves split into separate selectable regions.
- Planar part faces.

**Can't extrude:**
- **Construction geometry.**
- **Open profiles as solids.** Open curves need **Thin** or **Surface** creation type.
- **A region that isn't closed.** Look for tiny gaps or a missing coincident.

**Result types:**

| Result | Behavior | Needs |
|---|---|---|
| **New** | Every disjoint body becomes its own part. **Adjacent or touching regions extruded together fuse into one part.** Use **Extrude Individual** (FS) for touching tubes. | nothing |
| **Add** | Merges into touching parts. Onshape sometimes defaults to Add, so check it. | the merge scope (all parts by default) |
| **Remove** | Cuts. | a body in the merge scope to intersect; cutting air errors |
| **Intersect** | Keeps only the overlap. | overlapping bodies |

**End conditions:**
- **Blind**, **Symmetric** (Blind and Through-all only) and **second direction**.
- **Up to next** fails if nothing is hit or the profile isn't fully covered by the target.
- **Up to face** uses the target face's infinite surface.
- **Up to part / up to vertex / up to mate connector** (+ offset).
- **Through all.**
- Prefer Up-to references for lengths that should follow the layout.

**Other rules:**
- **Surface extrudes** support New and Add only.
- **One extrude can take many regions**, even from multiple sketches, which saves features. It can't give them different depths; use separate extrudes or Up-to.

## Other features

- **Revolve:** needs an axis (sketch line or edge), and the profile must not cross the axis.
- **Sweep:** profile + path. Use Pierce to tie the profile to the path. The profile must not self-intersect along tight bends.
- **Loft:** profiles (plus optional guides). Matching vertex counts lower the chance of twisting [verify].
- **Fillet / chamfer:** fails if the radius is bigger than the adjacent faces allow. Put them late; never reference their edges later.
- **Shell:** pick the faces to remove. Fails if the thickness exceeds the local geometry.
- **Hole:**
  - Places at sketch points, vertices, circle centers or mate connectors. It doesn't take bare regions.
  - Handles clearance, tapped, counterbore and countersink types. Use it when you need fastener semantics.
- **Patterns:**
  - The count **includes the seed**.
  - Types are Feature, Part and Face. Face is fastest; Reapply features is slow.
  - Circular patterns need an axis (edge, axis or mate connector). Linear patterns need a direction (edge or mate connector).
- **Mirror:** feature, part or face about a plane or planar face (a sketch *line* only works inside a sketch).
- **Sketch pattern / mirror / offset / trim / fillet:** these work only within the sketch.
- **Derive:**
  - One-way link. It can bring parts, sketches, curves, planes and mate connectors.
  - It can't derive from its own part studio, create circular references, or derive the same studio and configuration twice.
  - Version references need a manual update (blue icon).
- **Composite:** closed = constituents not selectable (reference bodies); open = still selectable.
- **Imported STEP/Parasolid:** dumb solids with no feature history. You can use them as references and do direct edits (Move/Delete/Replace face). You can't parametrically edit them. Prefer FRCDesignLib or the vendor's Onshape document.
- **Rollback:** a feature can only reference features above it. Features below the rollback bar don't exist yet.

## Assemblies

- **Mates:** exactly one mate joins two mate connectors (Fastened, Revolute, Slider, Cylindrical, Pin slot, Planar, Ball, Parallel, Tangent, Width).
- **Limits:** only on the mate's free degrees of freedom.
- **Mate connectors:**
  - Part Studio connectors can reference sketches and the origin, and every instance has them.
  - Assembly connectors can't reference sketch entities.
  - A mate connector's owner part decides what it moves with.
- **Group:** locks current relative positions; it doesn't follow later geometry changes. Grouped instances can't be the seed of Replicate. Subassemblies in a group must be rigid.
- **Replicate:** the seed needs exactly one external mate onto matching geometry.
- **Configurations:** assemblies can configure mates, instances and patterns, but **not mate connectors**. Configured Variable Studios can't be released.
- **Relations** (gear, rack & pinion, screw, linear): each links existing mates of the right type (rotational or linear).

## When a feature errors

1. **Read the error.** Common causes:
   - open region
   - Remove extrude with no intersecting body
   - Up to next with no target
   - over-constrained sketch
   - missing reference after an upstream change
2. **Fix the earliest red feature first** (see `cad-review`).
3. **Don't paper over an error** by suppressing the feature or adding another feature below it.
