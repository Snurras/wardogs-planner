# 02 · Design tools & building rules
Use for: toolbar tools, placing/stacking pieces, entrances, Wall Optimization, Guide/Bumper blocks, templates, map controls.

## Toolbar (one row down to ~1280 px; buttons tighten below 1440 px)
Select (V) · Brush (B) · Undo · Rotate (R) · Erase (E) · Modify structure (M) · Wall Optimization · Side view (S) | Clear (IED icon) · Straight lines (checkbox) · Auto elevation (checkbox, was Elevation Stacking).
- Coloured icons with text kept. Zoom (− size + Fit) and Grid labels sit **below** the map on the right.
- Process bar above: **1 · Design it → 2 · Haul it → 3 · Build it** (arrow steps with live summaries). Fact sheet / About on the right of the header.
- **Tools row** under the steps: Find designs, Structure designer (left); **Open ▾** (Find designs…, ★ Favourites, My designs), title field (`dTitle`, autofill off), Personal / Shared, **Save**, **⋯** (Delete, Save / Import .txt) on the right. Menus: `closePops`, `openKey`.
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
| Large Shelter (Season 02) | 6×6 | roof H3 (0.35 thick) on 4 corner pillars, open under it: pieces up to H2 go under it; pillar squares stay free |
| MG Nest (Season 02) | 1×1 | H1, emplacement, standing gunner, angles graded like the Talon (Fact sheet dgf.mg.*). **Free piece** (`P.free`): `p.off=[dx,dy]` (±0.5, steps 0.05) from its square's middle, Snap to grid checkbox (`snapGrid`), Alt+arrows nudge; only drawing and the gun pivot use it. **Inside piece** (`P.inside`): on a free square inside a structure, on a floor it fits under (`roomsIn`, roof 0.35), `p.in`, `p.fl` (floor, [ ] while placing), snaps to a window (`windowSnap`). `pickAt`, `insideOf`, `surfTarget` (threat check) |
| Wooden Step (Season 02) | 1×1 | wooden platform H0.2 (Fact sheet `ht.step.pct`), nothing builds on it |
| Loudspeaker 2×2 H3 · Builder's Radio 2×1 H1 | | |
| HESCO Small 1×1 H1 · Large 1×1 H2 · HESCO Wall 4×1 H2 | | |
| Bremer Wall 1×1 | face H3 (can't be jumped), footing H1 walkable | |
| Door 1×1 H2 · Gate 4×1 H3 (wire on top) | | |
| Sandbags 2×1 · Barbed Wire 2×1 · Hedgehog 2×2 · Recon Tent 3×2 | field | |
| FOB 3×3 | fixed, can be moved not erased | |

## Building rules (all numbers are facts, see Fact sheet)
- HESCO/Doors on HESCO/Doors up to H7; anything on a building up to H10. Bunker on ground or on HESCO ≤ H2. Recon Tower / Shelter on the ground only (but elevation can raise them to H1, see below).
- Ladders: nothing but a structure can be built on the square at a ladder's foot. **Game quirk (tested 12 Oct 2026, likely a bug):** a structure may be placed so it blocks its own ladder or another structure's ladder, e.g. next to a wall. Fact `rule.ladderStruct` (Stacking limits, *Structures may block a ladder*): 1 = allowed (today), 0 = refused both ways, for when the game fixes it.
- FOB build area: 60 m square centred on the FOB (field pieces may sit outside). One Refuel and one Repair Station per FOB.
- Gap rule (emplacements keep a 1-square clear gap) is **switched off**: its checkbox is hidden and every load turns it off. The code stays in case it comes back.
- **Elevation** (free foundation; checkbox **Auto elevation**, code `fndMode`, `p.fnd`): a piece snapped side-to-side to a piece standing on a small HESCO is built one level up for free; it chains; stays when the Bumper block is removed. Not for barbed wire, tents, hedgehogs, sandbags.
- **Guide blocks (GB) / Bumper blocks (BB)**: helper blocks for stacking; placed only (1 s, 1 supply). “Show Guide and Bumper blocks” checkbox under the notices hides their markers on the map (build steps keep them).

## Modify structure (M) — also closes entrances
- Toolbar button or M (or Select one structure → Modify in the selection bar). A bar opens under the toolbar: **Ground · Floor 2 · Roof** (always shown; Floor 2 greyed out on Bunker and Shelter, which have no middle floor; your own taller structures get Floor 3 …; [ ] change floor), the block to add (HESCO Large, HESCO Small, Door, Sandbags) and **Advanced**.
- **First click on a structure only picks it** (thick outline). Then: click a square = add the chosen block on that floor, or put back a removed block of that kind. E or right-click = take a block off with the hammer.
- Entrances (red arrows) and the open centre of Recon (2×2) / Shelter (3×3) are on the Ground floor: click closes them, E / right-click opens them. Recon / Shelter take the block you chose: HESCO Large or a Door become a seal (`p.closed` / `p.doors`), HESCO Small or Sandbags go in as an added block (the arrow is hidden under it). **Bunker**: only a HESCO Small fits (1.65 headroom), so it is picked for you and the message says so (`sealPick`).
- **Restore**: E or right-click on a block you took off makes it as built again (any block, Corner HESCO too; what fell with it comes back). Left click with the same block chosen still *puts it back* (stands, holds nothing up).
- **Holes** (a block taken off from the ground ring): drawn as a red square, no arrow (`entrancesOf` marks them `hole`); the red arrows stay on original entrances. A hole is a plain square in Modify: any block can be added there (a Door gets its preview and R).
- **Doors and Sandbags** added with Modify are drawn on the map as a Door symbol and a row of bags against one side of their two squares (R turns them through N, E, S, W; stored as `r` 0–3, the side in the structure's own turn).
- **Sandbags pieces** (Field) on the ground are drawn against the side they are turned to, on the map and in Side view (`bagsMark`, `bagsRect`); on top of a block they stay centred, as the protection maths assumes.
- Labels in Modify and the Structure designer: H1 HESCO Small, H2 HESCO Large, HX = HESCO X Size (the 1.65-high block that carries a roof; called Corner HESCO before 12 Oct 2026, code type `corner`). R turns a new Door before you place it, or the Door under the pointer (added ones, and Doors in an open centre). Sandbags may go into an **open** entrance (e.g. one made wider by taking a block off); a closed one must be opened first.
- **The chosen floor** (Ground too) is drawn over the structure on the map (`drawFloor`) in the Structure designer's look: HESCO / Corner as labelled blocks (HL, HS, CO), Sandbags as bags on the edge, Windows as a wooden frame on their sandbags, Doors as the door symbol; red dashed = taken off, dashed = fell, green rim = added; Ground also shows ENTRY / open centre and seals.
- **Windows blocked with Sandbags**: pick Sandbags and click a window. They are stored as an added block at the window's height (`[sandbags,x,y,window z,window r]`), standing on the sandbags under it (`addsStanding`: an added block stands on the ground, a slab, or a block still there). A filled window is no window (`winBlocked`): no crawling, gone from the threat check's weak points. Order to unblock: erase the added Sandbags, then the sandbags under the window. Structure designer: Sandbags may be placed in a window's space on its layer.
- **Headroom**: under a roof resting on Corner HESCO (inside the Bunker, Recon floor 2) there is 1.65 of room, so no HESCO Large or Door there (`addErr`).
- Taking off a block that brings more down (collapse rules, doc 11 §6) asks first. Pieces you placed normally on a part that falls go with it, and are listed in the warning. Undo brings it all back.
- Put-back blocks hold nothing up. Added blocks cost their normal supplies and build time; blocks taken off cost 7 s each (`t.remove`).
- Advanced: the chosen floor as a grid over the map, with the collapse rules and the list of changes.
- Side view (S) while modifying shows that structure. Brush and Wall Optimization are greyed out.
- Data: `p.mod = {rm, back, add}` (doc 11), entrance/centre seals in `p.closed`, `p.doors`, `p.doorR` (centre keys 100+). Sealed centres **do** block the threat check (doc 03). Helpers `entrancesOf`, `centreOf`, `windowsOf`, `ladderSpots`, `openingsOf`.

## Wall Optimization
Finds the most 4-in-a-row Large HESCO (any layer) and swaps each four for one HESCO Wall (DFS max packing per group, up to 6 passes; around a 3×3 FOB it makes the pinwheel). Re-seats stacked pieces, skips swaps that break rules, keeps the first block's build step. Green bubble under the button: “100 supplies and 90 s saved”.

## Other tools
- Select: pick, box-select, move, turn, delete, copy/paste (Ctrl+C/V); picking takes everything on top.
- Select → **Add elevation** / **Remove elevation** (selection bar; each shows only when it can act). Add raises selected ground pieces one level on a free foundation, with what stands on them. Each side-to-side group snaps to its earliest-built raised neighbour; groups with none get a Bumper block, chosen so one free square serves as many groups as possible (inside the FOB area, not on a ladder foot, away from the FOB). Each group is moved in the build order as a chain from its neighbour or Bumper block, so no extra Bumper blocks appear. A group that breaks a rule stays and the message says why; a small HESCO holding something up is left alone. Remove takes elevation off the selected pieces. Code: `addElevation`, `removeElevation`, `bumperPlan`, `chainFrom`, `orderChain`, `reseat`, `chainFnd`.
- Build order (`buildSteps`): a Bumper block already built next to a piece, on a square nothing stands on, is kept up for it (its remove step moves later) instead of a new one.
- Brush: eyedropper picks a stack (one or more squares), paints copies; transparent preview; rotate with R. With Auto elevation on, brushed ground pieces landing next to a raised piece are raised too, in chain order (`brushFnd`).
- Side view (S): see doc 04.
- Templates: removed (11 Oct 2026 c). Shared designs and Find designs do that job.
