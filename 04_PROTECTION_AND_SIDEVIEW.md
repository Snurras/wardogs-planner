# 04 · Protection pictures, Side view & 3D graphics
Use for: Direct ground fire protection rules, the emplacement hover picture, the Side view tool, and how pieces are drawn from the side.

## Direct ground fire protection (geometry from the weapon's pivot; facts group “Direct ground fire protection”)
| Weapon | Pivot height | Pivot to edge | Lowest angle | Checked out to |
|---|---|---|---|---|
| CIWS | 2h | 2 grids | −10° | 8 grids |
| L81 Mortar | 0h | 1 grid | 45° (2h at 1 grid out missed, 3h at 2 out barely hit) | 5 grids |
| Talon | 1h | 1 grid | 0° | 10 grids |
| Stingray | — | — | fixed 80° drone launch, never blocked | — |
- Angle = line from the pivot over the cover's top corners (Bremer: its real outline). Bands under 3° ignored.
- CIWS: ≤0° “some low angles blocked”, ≤15° limited, steeper poor. Talon: ≤5° all free, ≤20° limited, steeper poor.
- Mortar range: 700 m at 45°, −6 m per degree steeper (2h adjacent → 590 m; 2h+SB 1 out → 685 m). Game quirk: sandbags on a block right next to the mortar never stop it.
- Protection = lowest side's cover at any distance: <1h none, 1h low, 1h+SB or 2h good, 2h+SB or 3h+ strong. Open side → “Partly missing …”. Sandbags: 0.65h high, 20% of a grid wide, centred on the block.
- Bremer: wall 45% deep on its face side, footing 70% → 30% of 1h; seen end-on it's a full 3h block.
- Mixed cover on one side: all drawn (others faded); maths uses the worst.
- Code: `dgfSpec`, `dgfCellAngle`, `dgfRange`, `dgfEval`, `dgfMap`, `dgfBremerProf`.

## Hover picture (emplacements)
- Side view to scale, turned like the map: **W left / E right**, **R** turns to **N left / S right** (R then never turns a piece). Compass at top, “Press R to rotate view”.
- Corner labels per side: range or angle (green / orange / red) + a small shield for that side's protection; big shield top-left = overall protection. Badges under the picture. No sentence text.
- Weapon icons: CIWS (pedestal, turret, white dome, gun; operator at a terminal on a stand), Mortar (baseplate, tube, bipod; straight green/orange/red line with a shell in flight, gap before the shell), Talon (pedestal, seated operator with the tube over his shoulder, head tilts with the aim), Stingray (cream canister as tall as the soldier, red/dark bands, clamped tablet, tail-sitter drone above). Soldier 1.75h tall.
- Same screen size at any zoom; opens above / below / right / left of the emplacement, wherever it fits in the visible map; follows scroll.
- No coloured bars or dashed squares on the map (removed on request).

## Side view tool (S)
- Drag a rectangle → view covers the map with ✕. **3D look** (default since 10 Oct 2026, staging v119): the Structure designer's high camera, turned slightly so you look mostly along the view direction; pieces drawn back to front, cut at the edge of the marked area. Ground shows the grid and numbered rows (1 = front).
- R walks round clockwise: look N (W left, E right) → E → S → W; Shift+R back. Compass + text show the direction.
- **Layer ▼ ▲** (or [ ]): everything under that height under a grey veil; blocks crossing the layer are cut at it. **Hide above**: hides what is over the layer. A new area starts at H0.
- **3D** button: back to the old flat side view (remembered in this browser, `wd_sv3d`).
- Clicking Side view (or S) again → back to the map with the area kept as a dashed outline; again → same view. Esc = back to map. ✕, a new area, or another tool clears it. Zoom − / Fit / +.
- Structures (built-in, your own, Modify changes) are drawn from their blueprint blocks: corner HESCO 1.65, roof slab resting on it, windows as wooden frames, ladders, camo net on the top roof.
- Emplacements: weapon + soldier are the old 2D drawings standing upright, aimed at the worse of the left/right sides. Protection in the **real direction for all four sides**: faint blue fan per side; a limited side gets a dashed ground line out to the checked distance (red poor / orange limited) and its blocked angle (CIWS, Talon) or mortar range standing up in that direction. Stingray: one dashed 80° line.
- Field pieces in 3D: Sandbags (bags on both visible faces), Barbed wire (posts, strands, coil rings), Hedgehog (three beams), Recon tent (camo net on four poles).
- Code: `sv3dSvg(a,view,L,{cut})` (projection `YAW` 22°, `EL` 30°, `KZ`), `svRender3d`, `sv3dOn`, `svLayer`; the old picture is `svRender` below it. Prototype + review page: private artifact "Side View 3D Mockup".

## How pieces are drawn (3D boxes in each piece's own layout: `svPieceBoxes`, `svBoxes`, `svFrame`, `svDetail`; the 3D look uses the same boxes)
- Bunker: 2h HESCO walls; entrance 1.4h with HESCO above; windows 1–1.3h on the middle two squares (not on the entrance side); thin roof (no extra height); camo net.
- Recon Tower: ground ring 2h with entrances (1.4h assumed), bunker-style floor 2 with windows and the opening at the ladder, yellow ladder outside, 2×2 small HESCOs on top (gone when trimmed).
- Shelter: 2h ring, 2h entrances, thin roof, 3×3 small HESCOs on top (gone when trimmed).
- Door: full square, plank floor, wooden pillar in all 4 corners, single plank roof, door leaf at the front edge.
- Bremer: sandy concrete, wall on face side + sloping footing.
- Gate: concrete posts, two X-braced leaves (small door in the left), coils on V-brackets, yellow-black strip.
- Repair: wooden deck, red tool cabinets, bench with yellow toolboxes and compressor, tyres, sandbags.
- Refuel: steel skid on sandbags, tank in a steel frame, blue-grey cases, pump console.
- FOB: steel pallet, blue cases, screen, tall lattice mast with blue flag and wind spinner (mast is not cover).
- Drill Rig: tall lattice tower on 4 sandbag blocks, platform, antennas, generator box.
- Loudspeaker: steel frame tower on a slab, sandbag base, rusty corrugated walls, platform at 2h with ladder, 4 horns on top, roof.
- Builder's Radio: steel table, yellow radio, green cases under, sandbags behind.
- Accepted as is (flat icons): Sandbags, Barbed wire, Hedgehog, Recon tent.
- Reference mockup pages (private artifacts): Protection Picture Review, Side View Depth Options, Side View Icons.
