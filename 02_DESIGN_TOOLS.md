# 02 · Design tools & building rules
Use for: toolbar tools, placing/stacking pieces, entrances, Wall Optimization, Guide/Bumper blocks, templates, map controls.

## Toolbar (one row down to ~1280 px; buttons tighten below 1440 px)
Select (V) · Brush (B) · Undo · Rotate (R) · Erase (E) · Modify structure (M) · Wall Optimization · Side view (S) | Clear (IED icon) · Straight lines (checkbox) · Elevation Stacking (checkbox).
- Coloured icons with text kept. Zoom (− size + Fit) and Grid labels sit **below** the map on the right.
- Process bar above: **1 · Design it → 2 · Haul it → 3 · Build it** (arrow steps with live summaries). Structure designer / Fact sheet / About are links in the header, next to the title.
- R priority: Side view open → turns the view; hovering an emplacement → turns the protection picture; Modify structure → turns sandbags (or a door in an open centre); Brush → turns brush; Select → turns selection/paste; else turns the piece to place.
- E (key and button): Erase on; again → back to the piece you were using. In Modify structure, E switches to taking blocks off.
- Undo: also undoes Open and Clear (brings back the previous design's pieces, name, Only FOB and haul plan).

## Pieces (palette groups: Emplacements, Stations, Structures, Walls & entry, Field; “Space” and “Supply” (build supplies) columns)
| Piece | Size | Height |
|---|---|---|
| L81 Mortar · Stingray | 3×3 | emp |
| Talon 9K-SAM | 2×2 | emp |
| Vanguard CIWS | 4×4 | emp |
| Refuel / Repair Station | 2×2 | H2 |
| Drill Rig | 2×3 | H3 |
| Bunker | 4×4 | roof H2, one floor, 4 corner HESCO, sandbags + 6 windows, 1 Small HESCO, entrance S x1 |
| Recon Tower | 4×4 | edges H4, centre 2×2 H5, floor 2 at H2, outside ladder |
| Indirect Fire Shelter | 5×5 | edges H2, centre 3×3 H3 |
| Trimmed Recon / Shelter | same | flat H4 / H2 (centre removed, extra trim time); no longer in the piece list, only in older designs |
| Loudspeaker 2×2 H3 · Builder's Radio 2×1 H1 | | |
| HESCO Small 1×1 H1 · Large 1×1 H2 · HESCO Wall 4×1 H2 | | |
| Bremer Wall 1×1 | face H3 (can't be jumped), footing H1 walkable | |
| Door 1×1 H2 · Gate 4×1 H3 (wire on top) | | |
| Sandbags 2×1 · Barbed Wire 2×1 · Hedgehog 2×2 · Recon Tent 3×2 | field | |
| FOB 3×3 | fixed, can be moved not erased | |

## Building rules (all numbers are facts, see Fact sheet)
- HESCO/Doors on HESCO/Doors up to H7; anything on a building up to H10. Bunker on ground or on HESCO ≤ H2. Recon Tower / Shelter on the ground only (but Elevation Stacking can raise them to H1, see below).
- Ladders: the square at a ladder's foot must stay empty, both ways: nothing can be built there, and a structure can't be placed with its ladder square on a piece already there.
- FOB build area: 60 m square centred on the FOB (field pieces may sit outside). One Refuel and one Repair Station per FOB.
- Gap rule (emplacements keep a 1-square clear gap) is **switched off**: its checkbox is hidden and every load turns it off. The code stays in case it comes back.
- **Elevation Stacking** (free foundation): a piece snapped side-to-side to a piece standing on a small HESCO is built one level up for free; it chains; stays when the Bumper block is removed. Not for barbed wire, tents, hedgehogs, sandbags.
- **Guide blocks (GB) / Bumper blocks (BB)**: helper blocks for stacking; placed only (1 s, 1 supply). “Show Guide and Bumper blocks” checkbox under the notices hides their markers on the map (build steps keep them).

## Modify structure (M) — also closes entrances
- Toolbar button or M (or Select one structure → Modify in the selection bar). A bar opens under the toolbar: **Layer 1, 2, 3…** (one per floor/roof of that structure: Bunker and Shelter 2, Recon Tower 3), the block to add (HESCO Large, HESCO Small, Door, Sandbags) and **Advanced**.
- **First click on a structure only picks it** (thick outline). Then: click a square = add the chosen block on that layer, or put back a removed block of that kind. E or right-click = take a block off with the hammer.
- Entrances (red arrows) and the open centre of Recon (2×2) / Shelter (3×3) are on Layer 1: click closes them with the chosen block, E / right-click opens them. **Only the right block closes them**: Bunker HESCO Small; Recon / Shelter HESCO Large or Door (your own structures: what their designer set). A wrong choice is refused with a message, never swapped.
- Taking off a block that brings more down (collapse rules, doc 11 §6) asks first. Pieces you placed normally on a part that falls go with it, and are listed in the warning. Undo brings it all back.
- Put-back blocks hold nothing up. Added blocks cost their normal supplies and build time; blocks taken off cost 7 s each (`t.remove`).
- Advanced: the chosen layer as a grid over the map, with the collapse rules and the list of changes.
- Side view (S) while modifying shows that structure. Brush and Wall Optimization are greyed out.
- Data: `p.mod = {rm, back, add}` (doc 11), entrance/centre seals in `p.closed`, `p.doors`, `p.doorR` (centre keys 100+). Sealed centres **do** block the threat check (doc 03). Helpers `entrancesOf`, `centreOf`, `windowsOf`, `ladderSpots`, `openingsOf`.

## Wall Optimization
Finds the most 4-in-a-row Large HESCO (any layer) and swaps each four for one HESCO Wall (DFS max packing per group, up to 6 passes; around a 3×3 FOB it makes the pinwheel). Re-seats stacked pieces, skips swaps that break rules, keeps the first block's build step. Green bubble under the button: “100 supplies and 90 s saved”.

## Other tools
- Select: pick, box-select, move, turn, delete, copy/paste (Ctrl+C/V); picking takes everything on top.
- Brush: eyedropper picks a stack (one or more squares), paints copies; transparent preview; rotate with R.
- Side view (S): see doc 04.
- Templates: the built-in list is empty; templates are designs the admin saves online (Open → Templates). Heights are worked out on load.
