# 02 · Design tools & building rules
Use for: toolbar tools, placing/stacking pieces, entrances, Wall Optimization, Guide/Bumper blocks, templates, map controls.

## Toolbar (one row, fits down to ~1180 px)
Select (V) · Brush (B) · Undo · Rotate (R) · Erase (E) · Modify an entrance (M) · Wall Optimization · Side view (S) | Clear (IED icon) · Elevation Stacking (checkbox).
- Coloured icons with text kept. Zoom (− size + Fit) and Grid labels sit **below** the map on the right.
- Process bar above: **1 · Design it → 2 · Haul it → 3 · Build it** (arrow steps with live summaries). Fact sheet / About by the title.
- R priority: hovering an emplacement → turns the protection picture; Modify an entrance → turns a centre door; Brush → turns brush; Select → turns selection/paste; else turns the piece to place.

## Pieces (palette groups: Emplacements, Stations, Structures, Walls & entry, Field; “Space” and “$” columns)
| Piece | Size | Height |
|---|---|---|
| L81 Mortar · Stingray | 3×3 | emp |
| Talon 9K-SAM | 2×2 | emp |
| Vanguard CIWS | 4×4 | emp |
| Refuel / Repair Station | 2×2 | H2 |
| Drill Rig | 2×3 | H3 |
| Bunker | 4×4 | roof H2, one floor, 4 corner HESCO, sandbags + 6 windows, entrance S x1 |
| Recon Tower | 4×4 | edges H4, centre 2×2 H5, floor 2 at H2, outside ladder |
| Indirect Fire Shelter | 5×5 | edges H2, centre 3×3 H3 |
| Trimmed Recon / Shelter | same | flat H4 / H2 (centre removed, extra trim time) |
| Loudspeaker 2×2 H3 · Builder's Radio 2×1 H1 | | |
| HESCO Small 1×1 H1 · Large 1×1 H2 · HESCO Wall 4×1 H2 | | |
| Bremer Wall 1×1 | face H3 (can't be jumped), footing H1 walkable | |
| Door 1×1 H2 · Gate 4×1 H3 (wire on top) | | |
| Sandbags 2×1 · Barbed Wire 2×1 · Hedgehog 2×2 · Recon Tent 3×2 | field | |
| FOB 3×3 | fixed, can be moved not erased | |

## Building rules (all numbers are facts, see Fact sheet)
- HESCO/Doors on HESCO/Doors up to H7; anything on a building up to H10. Bunker on ground or on HESCO ≤ H2. Recon Tower / Shelter on the ground only. Nothing on the square in front of a structure's ladder.
- FOB build area: 60 m square centred on the FOB (field pieces may sit outside). One Refuel and one Repair Station per FOB.
- Emplacements keep a 1-square clear gap (gap rule).
- **Elevation Stacking** (free foundation): a piece snapped side-to-side to a piece standing on a small HESCO is built one level up for free; it chains; stays when the Bumper block is removed. Not for barbed wire, tents, hedgehogs, sandbags.
- **Guide blocks (GB) / Bumper blocks (BB)**: helper blocks for stacking; placed only (1 s, 1 supply). “Show Guide and Bumper blocks” checkbox under the notices hides their markers on the map (build steps keep them).

## Modify structure (selection bar, one structure selected)
- Panel over the map: pick a layer, click a block to take it off with the hammer, click a removed block to put it back. Warns before anything more than the block falls (can't be undone in game). Put-back blocks hold nothing up. Collapse rules and code: doc 11 §6 and §11.

## Entrances (Modify an entrance, M)
- Red arrows = entrances. Recon/Shelter: seal with Large HESCO or Door; Bunker: Small HESCO only. Cycle: open → HESCO → Door → open.
- The open centre of Recon (2×2) and Shelter (3×3), full or trimmed, can be closed like entrances (keys 100+); thin red grid shows them while the tool is on. R turns a centre door. Not used by the threat check.
- Data: `p.closed`, `p.doors`, `p.doorR`; helpers `entrancesOf`, `centreOf`, `windowsOf`, `ladderSpots`.

## Wall Optimization
Finds the most 4-in-a-row Large HESCO (any layer) and swaps each four for one HESCO Wall (DFS max packing per group, up to 6 passes; around a 3×3 FOB it makes the pinwheel). Re-seats stacked pieces, skips swaps that break rules, keeps the first block's build step. Green bubble under the button: “100 supplies and 90 s saved”.

## Other tools
- Select: pick, box-select, move, turn, delete, copy/paste (Ctrl+C/V); picking takes everything on top.
- Brush: eyedropper picks a stack (one or more squares), paints copies; transparent preview; rotate with R.
- Side view (S): see doc 04.
- Templates exist (heights worked out on load).
