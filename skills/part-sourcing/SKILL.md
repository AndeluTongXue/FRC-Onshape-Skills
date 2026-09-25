---
name: part-sourcing
description: Finds FRC parts online and extracts trustworthy dimensions, specs, and CAD for Onshape modeling — searching WCP, SDS, REV, AndyMark, Thrifty Bot, CTRE, VEX, McMaster-Carr, Redux, and others; reading spec tables and drawing PDFs; choosing FRCDesignLib vs vendor Onshape docs vs STEP; and recording part numbers. Use when asked to "find a part", "what are the dimensions of", "get CAD for", pick COTS hardware, check a bearing/motor/module footprint, or when a design needs a real part number.
---

# Part Sourcing

> - **Tree:** `frc-cad-foundations` › Plan › **part-sourcing**
> - **Also load:** `tolerances` for fits when modeling to the numbers
> - **Next:** back to the task that needed the part

The job: get **correct numbers from a primary source** and the **lightest usable CAD**, and record where each came from.

## Search order for CAD

1. **FRCDesignLib (via FRCDesignApp)**: simplified, configurable, Onshape-native. This is the default for COTS in assemblies. It can't search by vendor part number, so search by name and vendor filter.
2. **Vendor's public Onshape document**: REV (most parts), Thrifty Bot (some kits), WCP (Competitive Concept robots only). Insert by version or derive.
3. **Vendor STEP**: import it into a separate reference document. Imported STEP has no feature history and is heavy, so simplify it or use it only to measure.
4. **Onshape Standard Content**: only standard bolts, nuts, washers, keys and PEM fasteners. It has no bearings and no FRC parts.
5. **Model it yourself** from the vendor drawing: a simple block or profile that carries only the interfaces (bolt pattern, bore, OD, width).

## Where the numbers are (per vendor)

See `references/vendors.md` for URL patterns, SKU formats, and what's readable.

| Vendor | Best dimension source |
|---|---|
| **REV** | Product page spec tab + PDF drawing + Onshape link (easiest for agents) |
| **WCP** | docs.wcproducts.com "Physical Specifications" pages; drawings/STEP on wcproducts.info |
| **SDS** | Product page "Layout Drawing" PDF (Shopify CDN); CAD on Google Drive (blocked for fetchers) |
| **AndyMark** | Product page spec list + "Layout Print" PDF + STEP |
| **TTB** | Product "Design Documentation" block; some Onshape docs |
| **CTRE** | store.ctr-electronics.com user guide PDF; ctre.download CAD zip (Kraken CAD: use WCP) |
| **McMaster** | Spec table + drawing, but pages are unreadable by fetch tools and CAD needs a login |
| **VEX** | Spec text on page; downloads widget is JS-only; many items discontinued |

## Procedure

1. **Identify the exact variant** before looking up any number: motor version, ratio, bore profile (hex vs rounded hex vs spline), hole size, and revision (e.g. NEO V1.0 vs V1.1; MK4i frame holes changed from 8-32 to 10-32 in June 2023).
2. **Find the page.**
   - Search with the site filter: `site:revrobotics.com MAXSpline bearing`, `site:wcproducts.info WCP-0783`, `site:docs.wcproducts.com Kraken`.
   - Shopify vendors (WCP, SDS, AndyMark, TTB, CTR store): append `.json` to a product URL for variants and SKUs. It doesn't include CAD links.
3. **Read the primary source, not a reseller or forum.** When reading a drawing PDF with a fetch tool, ask for **each value with its label and units**. Parsers drop labels and swap values.
4. **Sanity-check** every critical number against a second source (spec table vs drawing, or vendor vs FRCDesignLib model). Examples of values that should raise a flag: a motor "pilot" of 0.313", a 1/2" hex bearing whose OD isn't about 1.125".
5. **Blocked sites** (McMaster, Google Drive, Amazon, Misumi CAD, VEX downloads):
   - Search the part number to find the description.
   - Ask the user to paste the spec table or upload the STEP/PDF.
   - Never scrape around a block.
6. **Record the result** in a note next to the part: vendor, part number or SKU, URL, the dimensions used, and the date checked. In the CAD, put the part number in the part's properties (not in its name).
7. **Model to the numbers.** Apply team fits from `tolerances` (e.g. bearing bore, sliding fits), and dimension the values directly in the sketch.

## Gotchas

- **Hex is not rounded hex.** 1/2" rounded hex = 13.75 mm (0.541"); 3/8" rounded hex = 10.25 mm (0.403"). ThunderHex, MAXSpline, SplineXL and SplineXS are separate profiles.
- **Hex shaft and bore tolerances differ by vendor.** One vendor's hex may not fit another's bearing. Check both parts.
- **Units:** REV lists metric first; WCP drawings show inches [mm]; sensors (Grapple, PWF) are metric (M3). FRC structure is imperial (#10-32, 2x1).
- **Configurable kits** (gearboxes, swerve modules): the CAD and dimensions depend on the motor, ratio, and wheel choice. Some SDS modules have mirrored layouts (MK5n Layout A/B).
- **Discontinued or moved items:** VEXpro products moved to WCP; WCP "Reference Only" pages are sold elsewhere.
- **Weights:** use the vendor's weight for the mass budget. Set it in the part's properties if the CAD's mass is wrong.

## Quick reference: common parts

These were verified from vendor pages in Sept 2026 and are in `references/vendors.md`. Re-check before manufacturing.

- **1/2" hex flanged bearing (FR8 style):**
  - 1.125" OD, about 1.225" flange OD, 0.313" overall width, 0.0625" flange.
  - WCP-0783, am-2986, REV-21-1915.
- **Kraken X60 (WCP-0940):**
  - Ø60 mm body, 3/4" pilot.
  - 11 × #10-32 holes on a 2.000" bolt circle, 30° apart, 0.250" deep.
  - SplineXS 8 mm shaft.
- **NEO Vortex (REV-21-1652):** #10-32 on a 2" bolt circle.
- **NEO V1.1 (REV-21-1650):** Ø60 mm body, 8 mm keyed shaft, 0.75" pilot, #10-32 on a 2" bolt circle. Check the drawing for the hole count.
- **CIM-class motors in general:** 2.5" (or 60 mm) OD, #10-32 on a 2" bolt circle.
- **SDS MK4i / MK5i / MK5n:**
  - Mount to 2x1 tube with 10-32 holes.
  - Footprint and wheel offset: take them from the layout drawing or STEP. Don't use remembered values.
