# 11 · Structures built from blocks + Structure Builder (plan)
Use for: rebuilding Bunker, Recon Tower and Indirect Fire Shelter as real blocks; the Structure Builder (admin); modifying structures in a design; new structures from game updates.
**Status (10 Oct 2026): Structure designer on staging (v110); the base map still uses the old structures. Recon Tower collapse rules confirmed in game (section 6.1).** Read with 01 (+ 03 for the threat check, + 04 for Side view).

**How to read this doc:** everything ending in **?** is an assumption. Snurra checks it in the game and deletes the ? (true) or corrects it. Section 10 has the questions that can't be guessed.

---

## 1. Why
Today each structure is one big piece with special rules: height maps, "raised"/"trimmed" areas, separate Trimmed pieces, lists of entrances, windows and ladders, and separate floor maps in the threat check. The code asks "is this a Recon Tower / Bunker?" in about twenty places. The game will add several more buildings, so this gets worse with every update.

## 2. What structures really are (Snurra, 9 Oct 2026)
- Structures are **mostly normal HESCO** with the same properties: **4 C4 per HESCO**, same heights.
- A few **special parts** that can't be built on their own: **floor, roof (also the middle floor), window, ladder**. They have **no C4 of their own**: they are destroyed only when the whole structure collapses.
- **Sandbags under the windows** are normal Sandbags (2×1, H1). Sandbags get **1 C4** (to add to the Fact sheet; today they have 1 there already?).
- **Entrances are just a missing block** in the wall. Sealing an entrance = putting a block in the gap.
- **Collapse:** not one rule but two, per floor/roof (tested on the Recon Tower 10 Oct 2026, see section 6): a **floor falls when too few ground HESCO are left**, a **roof falls when too few of its supports are left**. Ground HESCO never fall from a collapse.
- **Build time and cost** belong to the structure as a whole (set in the Structure Builder), not to its blocks.

## 3. The idea
- A structure is a **blueprint**: blocks placed layer by layer, exactly as in the game.
- **Structure Builder** (admin only): a design tool where Snurra builds a structure from normal blocks + special parts, sets its properties and saves it. It then shows up in the Structures palette for everyone.
- Placing a structure is still one click, and it stays **one thing** in the planner (select, move, rotate, erase, brush, build order).
- Users can **Modify** a placed structure: pick a layer, then add blocks in free spots or remove parts. This is possible in the game but not supported by the planner today.
- The threat check, Side view, protection pictures and a future 3D view all read the blocks. They never need to know which structure it is.

## 4. Building blocks
| Block | Normal or special | Size | C4 | Notes |
|---|---|---|---|---|
| HESCO Small / Large | normal | 1×1, H1 / H2 | 4 | as today |
| Sandbags | normal | 2×1, H1 | 1 | under windows |
| Door | normal | 1×1, H2 | 1 | to seal an entrance |
| **Floor** | special | 1×1, thin | — | the ground floor slab; does it raise the inside by anything? |
| **Roof** | special | 1×1, thin | — | walkable on top; also used as the **middle floor** (Recon floor 2) |
| **Window** | special | 1×1 or 2×1, H1? | — (part of the structure) | sits on sandbags; crawl in level with that floor after blowing the sandbags under/around it? |
| **Ladder** | special | on a square's outer edge | — | leads to the floor at its top; no C4 |

**The only really new thing for the planner is the roof slab**: a block with **open space underneath** (people can walk under it and stand on it). Everything else is already HESCO the planner knows. So the "squares get floors" change in the threat check is smaller than first planned: only roof slabs make hollow columns.

## 5. Blueprints (facing north, rotation 0; x = column 0 → east, y = row 0 → south)

### Recon Tower 4×4 (the most complex one)
Build order, as in the game:
1. **Floor** on all 16 squares.
2. **10 Large HESCO** (H0–H2) round the outer ring; the 2 gaps are the entrances (W y2, E y1).
3. **Middle floor / roof** at H2 on all 16 squares?
4. **Floor 2 walls**: 4 special Large HESCO (1.65 high) in the corners + 1 Small HESCO next to the ladder opening (S x2).
5. **Sandbags** between the corners: N x1–x2, W y1–y2, E y1–y2 (3 Sandbags, 2×1 each).
6. **Windows** on top of the sandbags (6 squares).
7. **Roof** at H4 on all 16 squares.
8. **4 Small HESCO** on the centre 2×2 (H4–H5).
9. **Ladder** on the south side at x1, up to floor 2.
```
Ground floor (H0–H2)          Floor 2 (H2–H4)               Roof (H4–H5)
    x0 x1 x2 x3                   x0 x1 x2 x3                   x0 x1 x2 x3
y0  H  H  H  H                y0  H  W  W  H                y0  r  r  r  r
y1  H  .  .  E                y1  W  .  .  W                y1  r  s  s  r
y2  E  .  .  H                y2  W  .  .  W                y2  r  s  s  r
y3  H  H  H  H                y3  H  L  h  H                y3  r  r  r  r
H = Large HESCO   h = Small HESCO   E = entrance (gap)   . = room   W = sandbags + window
L = ladder opening   r = roof   s = Small HESCO on the roof
```
- **Confirmed in game (10 Oct):** ground floor ring as drawn, entrances at W y2 and E y1 (10 ground HESCO). Floor 2 corners are **special Large HESCO, 1.65 high** (+ the 0.35 roof slab = 2); they carry the roof and **can't be built by players from the middle floor**. The block at **S x2 is a Small HESCO** with a small gap under the roof: it does **not** carry the roof.
- Snurra's test labels: rows **A–D = y0–y3**, columns **1–4 = x0–x3** (A1 = NW corner, ladder under D2).
- Floor 1 and floor 2 are not connected inside (no stairs)?
- Floor 2 room is only the centre 2×2? (The ring is walls, windows and the ladder square.)
- **Trimmed Recon = remove the 4 Small HESCO on the roof** (4 × 7 s ≈ the 30 s trim time). No separate piece any more.
- Total: 10 + 5 = 15 Large HESCO, 4 Small HESCO, 3 Sandbags, 6 windows, 1 ladder, floor, middle floor, roof.

### Indirect Fire Shelter 5×5
1. Floor on all 25 squares.
2. **12 Large HESCO** round the ring; 4 gaps = entrances in the middle of each side.
3. Roof at H2 on all 25.
4. **9 Small HESCO** on the centre 3×3 (H2–H3).
```
Ground floor (H0–H2)          Roof (H2–H3)
    x0 x1 x2 x3 x4                x0 x1 x2 x3 x4
y0  H  H  E  H  H             y0  r  r  r  r  r
y1  H  .  .  .  H             y1  r  s  s  s  r
y2  E  .  .  .  E             y2  r  s  s  s  r
y3  H  .  .  .  H             y3  r  s  s  s  r
y4  H  H  E  H  H             y4  r  r  r  r  r
```
- No windows?
- **Trimmed Shelter = remove the 9 Small HESCO** (9 × 7 s ≈ the 60 s trim time).

### Bunker 4×4 · roof H2
Today: 1 C4 for the outer wall, windows on every outer square except the entrance. That matches **sandbags + windows**, not HESCO:
1. Floor on all 16 squares.
2. **Sandbags (H1) with a window on top** round the ring: 15 squares → 7 Sandbags (2×1) + 1 single square? The gap at S x2 is the entrance?
3. Roof at H2 on all 16.
```
Ground floor (H0–H2)
    x0 x1 x2 x3
y0  W  W  W  W
y1  W  .  .  W
y2  W  .  .  W
y3  W  W  E  W        W = sandbags + window, E = entrance (seal with Small HESCO only)
```
- Is the ring really sandbags + windows, or HESCO with windows? (This decides 1 or 4 C4.)
- The inside 2×2 is room?
- Collapse rule for the Bunker: it has no HESCO on the ground floor, so what makes it fall?

### Not structures in this sense (stay normal pieces)
Loudspeaker, Builder's Radio, Bremer, Door, Gate, stations, emplacements?

## 6. Collapse
### 6.1 Recon Tower: confirmed in game (Snurra, hammer tests 3–10, 10 Oct 2026)
Labels as in section 5: A–D = rows y0–y3, 1–4 = columns x0–x3. Ground HESCO (10): A1 A2 A3 A4 · B1 · C4 · D1 D2 D3 D4. Pillars = the floor 2 blocks on A1, A4, D1, D4 (corners, carry the roof) and D3 (Small HESCO, does not touch the roof).
1. **Remove a ground HESCO under a pillar** → that pillar and its square of middle floor fall. Under a sandbags/window square (A2, A3, B1, C4, D2) → nothing falls.
2. **Roof falls when 2 of the 4 corner pillars are gone.** The roof's 4 Small HESCO and the windows go with it. Floor 2 and the sandbags stay. D3 doesn't count.
3. **Floor 2 falls when 5 or fewer ground HESCO are left** (of 10). Middle floor, sandbags and ladder go. Pillars still standing and all ground HESCO stay. Windows keep hanging from the roof if it is still up.
4. Roof and floor 2 are **independent**: either can fall first. The order of removals doesn't matter, only which blocks are gone.
5. **Ground HESCO never fall** from a collapse.
6. **C4 is different:** the blast also destroys the next HESCO (tests 1–2: C4 on D3 took D4 too). How far the blast reaches is not measured yet.

Useful trick (test 7): with A2, A3, D2, D3, C4, D4 + one more gone, the roof still stands on A1, A4, D1: an open, roofed space (e.g. a mortar under the roof).

### 6.2 What this means for the planner
- A structure needs **two kinds of rule**, set in the Structure Builder:
  - **Floor rule:** "this floor falls when the ground HESCO drop to N" (Recon floor 2: N = 5).
  - **Roof rule:** "this roof falls when its supports drop to N", with the supporting blocks marked (Recon roof: the 4 corner pillars, N = 2).
- A block falls when the block it stands on is gone (pillar on a ground HESCO). What falls with a floor or roof (sandbags, ladder, windows, roof HESCO) is part of the rule.
- The threat check can use it: blowing 2 corners clears the Recon roof; 5 ground HESCO clear floor 2. The attack animation shows it falling.

### 6.3 Tests still to run (hammer only)
Before each structure: draw its ground floor like the Recon (block name per square, `00` for a gap) and say what sits on top. Note after **every** removal what fell.

**Indirect Fire Shelter** (12 Large HESCO, 4 gaps, roof at H2 with 9 Small HESCO on top)
- **S1 corners first:** remove the NW corner, then the SE corner, then the other two. Does the roof (or part of it) fall at 2 corners, like the Recon?
- **S2 sides first** (new Shelter): remove the 8 side HESCO one by one, going round, before any corner. When does the roof fall, and does it fall all at once or square by square?
- **S3 one side:** remove all 3 HESCO on the north side (NW, N, NE). Does only that edge of the roof fall?

**Bunker** (first check: is the ring HESCO, or sandbags + windows? How many C4 does the game show for one ring square?)
- **B1 corners first:** remove 2 corners, then the other 2. When does the roof fall?
- **B2 sides first** (new Bunker): remove the side blocks one by one before any corner. Count left when the roof falls.

**Filled gaps and rebuilt HESCO** (Recon; these decide whether players can make a structure stronger)
- **F1 filled entrance counts?** Fill the entrance C1 with a Large HESCO. Then remove A2, A3, B1, C4, D2. Prediction if it counts: 6 left, floor 2 stands. Then remove D3: floor 2 falls.
- **F2 HESCO in the room counts?** New Recon: put a Large HESCO in the room at B2 (under the middle floor). Same removals as F1. Does it hold floor 2 up?
- **F3 rebuilt corner:** remove D4 (its pillar falls), build a new Large HESCO at D4. The pillar can't be rebuilt, so the prediction is: removing A1 next drops the roof (2 corners gone). Does the rebuilt D4 count for the floor 2 rule?

Still open: how far a C4 blast reaches (one block, or a radius?).

## 7. Structure Builder (admin)
- A new design tool, only visible to the admin. Works like the normal map but on a small grid for one structure.
- **Build layer by layer**, starting from the bottom: pick a layer, click to place normal blocks and special parts. The layers below show faded. Side view (and later 3D) as a preview.
- **Properties to fill in:** name, short name, size, build supplies, build time, hammer tier, trim time (if it has a top that can be removed), ground only / allowed on HESCO up to H?, collapse rule (block type + number), which blocks are the "trim" blocks.
- **Entrances need no setting**: a gap in the wall at ground level is an entrance. What may seal it (Large HESCO, Door, Small HESCO only) is a property?
- **Save** like a design: to **test** first (`test_structures`), check it, then **publish to live** (`structures`). Firebase rules: only the admin can write. Everyone can read.
- **Changing a published structure** updates every design that uses it. A user's changes that no longer fit (e.g. HESCO added in a spot that is now a wall) are dropped with a notice.
- Parts can be **copied between structures** (e.g. reuse the Recon floor 2 in a new building). Later maybe saved as parts of their own.

## 8. Modify a structure (users)
- Click a placed structure → **Modify** → pick a layer → add blocks in free spots or remove parts (normal blocks only? special parts go only with collapse?).
- Replaces today's **Modify an entrance (M)** and the centre seals: sealing an entrance or the centre is just adding a block there.
- Removing too many ground-floor HESCO shows a warning: "This structure collapses".
- Supplies and build time: the structure's own numbers + normal blocks added (normal cost) + removals (7 s each, like trimming).
- Saved as **structure + changes** ("Recon Tower at X; removed: the 4 roof HESCO; added: Door at W y2"), not every block. Saves stay small and pick up fixes to the blueprint.
- Old saves (`recon_trim`, `ifs_trim`, `closed`, `doors`) load as the matching structure + changes.

## 9. Plan of work (each step can go on test by itself)
1. **Block model inside the threat check.** Roof slabs with space underneath; the three structures written as blueprints in code. No visible change. Compare old and new threat check on all templates and some saved designs until they match.
2. **Heights, Side view, protection pictures** read the blocks. Remove the old special code (height maps, `raised`/`trimmed`, `bld`/`bld2`/`flr`/`cseal`, the Trimmed pieces).
3. **Modify a structure** for users (section 8) + collapse in the threat check and the attack animation.
4. **Structure Builder** for the admin + saving structures to Firebase (test → live). From then on, new buildings need no code unless they bring something new (stairs, hatches, turrets…).
5. **3D view** (optional): every block type gets one 3D look; structures come for free.

Code today (v105, see 01 code map): piece catalogue `P` (`bunker`, `ifs`, `recon_tower`, `recon_trim`, `ifs_trim`, ~line 979); heights from the Fact sheet ~line 1085; entrance / centre / window / ladder helpers ~line 1094–1130; `threatGrid()` ~line 2850; Side view drawing of buildings ~line 1866.

## 10. Questions for the game
Answer as a short text list + 1–2 photos. Correct any **?** above at the same time.
1. **Collapse:** ~~Recon Tower~~ answered (section 6.1). Shelter and Bunker: run the tests in 6.3.
2. **After collapse:** ~~Recon~~ answered: ground HESCO stay, sandbags stay when only the roof falls. Do pieces a player built on top fall?
3. **Before collapse:** ~~Recon~~ answered (section 6.1). Can you walk in through the hole? (D2 removed: no, the ladder blocks it.)
4. **Recon floor 2:** Large HESCO (H2–H4) in the corners? The extra one at S x2? Floor 2 room only the centre 2×2?
5. **Windows:** height H1 on top of H1 sandbags? Blow the sandbags (1 C4) and crawl in, or blow the window?
6. **Bunker ring:** sandbags + windows, or HESCO? 1 or 4 C4 to get in?
7. **Floor:** does the floor raise the inside at all, or is it at H0?
8. **Modify in game:** what can be added to a structure (HESCO in the centre, on the roof, in entrances, on floor 2)? What can be removed with the hammer besides the roof HESCO?
9. **Rebuild:** can a blown HESCO in a structure be rebuilt as a normal HESCO, and does the structure count as whole again?
10. **Shelter:** any windows or firing slits?
11. **New buildings:** name + size + 1–2 photos of each new one is enough to try the Structure Builder on.

## 11. Structure designer (on staging, 9 Oct 2026)
- Opened from the **Structure designer** link under the piece list (above Legend). Own section `#tab-structs` (`showTab('structs')`), module `<script id="wd-structs">` at the end of the file. "Map" goes back.
- Toolbar reuses the planner's Undo, Rotate, Erase and Clear buttons (icons copied at start-up) + Trim parts (T) + Test C4. Palette rows look like the planner's (Space, $). Keys R, E, T, [ ], Ctrl+Z, Esc are caught while the section is open.
- Blocks: HESCO Small / Large, Sandbags (2×1, on one edge, 50 % deep), Door; special: Floor (H0), Roof / middle floor (thin, walkable, open space under), Window (2×1 wooden frame on the edge, 20 % deep, H1, no glass: a 1h opening = crawl only), Ladder (outside edge of a square, up to its layer). R picks the edge / side.
- Corrections from Snurra 9 Oct: windows are a wooden frame 2 wide, no glass, on the edge; sandbags on the edge, half as thick as HESCO.
- Map: the layer you are on full colour, what is below faded with its height, blocks from below hatched, floor/roof dotted, entrances found automatically (gap in the ground ring). 3D view: isometric, turnable, everything under the current layer under a grey veil; "Cut above layer".
- Check panel: size, highest point, floors, entrances, windows, ladders, block counts, trim parts vs trim time, C4 for all normal blocks, collapse status.
- Saving (`ST`, `entriesSt`): **Examples** (built in), **Published** (admin; everyone sees), **My structures** (personal). Firebase `structures` / `test_structures` docs `{owner, ownerName, visibility:'personal'|'published', name, data (JSON), updated}`; in claude.ai the page database `structures`; without either, this browser (`wd_structures`). Blueprint data: copy/paste JSON `{v:1, name, short, tier, supplies, build, trim, seal, ground, maxbase, cmin, ctype, blocks:[[type,x,y,z,(r),(trim)]]}`.

### Firebase rules to add (Firestore, Rules tab)
```
function isAdmin() { return request.auth != null && exists(/databases/$(database)/documents/admins/$(request.auth.uid)); }
function structOk(d) {
  return d.keys().hasOnly(['owner','ownerName','visibility','name','data','updated'])
    && d.owner == request.auth.uid && d.name is string && d.name.size() <= 40
    && d.data is string && d.data.size() < 200000
    && (d.visibility == 'personal' || (d.visibility == 'published' && isAdmin()));
}
match /structures/{id} {
  allow read: if resource.data.visibility == 'published' || (request.auth != null && resource.data.owner == request.auth.uid);
  allow create: if request.auth != null && structOk(request.resource.data);
  allow update: if request.auth != null && structOk(request.resource.data) && (resource.data.owner == request.auth.uid || isAdmin());
  allow delete: if request.auth != null && ((resource.data.owner == request.auth.uid && resource.data.visibility != 'published') || isAdmin());
}
match /test_structures/{id} {   // same, testers only
  allow read: if request.auth != null && exists(/databases/$(database)/documents/testers/$(request.auth.uid))
    && (resource.data.visibility == 'published' || resource.data.owner == request.auth.uid);
  allow create, update: if request.auth != null && exists(/databases/$(database)/documents/testers/$(request.auth.uid)) && structOk(request.resource.data);
  allow delete: if request.auth != null && ((resource.data.owner == request.auth.uid && resource.data.visibility != 'published') || isAdmin());
}
```
If the rules already have an `isAdmin()` function, keep the existing one and skip that line.

### Placing them on the base map (staging v111, on test 10 Oct 2026)
- Card under the Structure designer link (`#stPlace`): drop-down of Published + My structures, and an icon button with the short name → `setTool('cs_…')`, place like any building.
- `<script id="wd-custom">` (before `wd-app`): `registerCustom(id, blueprint)` builds a normal piece type in `P` from the blueprint: footprint, height map (`hm`), entrances = floor squares on the edge with no ground block, windows (side from the window's edge, `winZ` = the floor under it; windows above ground make it two-floor like the Recon), ladder, `seal`, ground only / `maxbase`; cost, build time, hammer and wall C4 go into `WD.DEF` (`b.` `t.` `h.` `c4.` + id). Not shown in the normal palette.
- Threat check: `two` also true for custom two-floor structures, floor 2 height via `WZ(p)`; windows of any custom structure count.
- Saved designs carry the blueprints they use (`design.customs`), registered again on load and from the draft, so a shared design opens for others.
- Known gaps: Side view draws them as plain HESCO blocks; no trim on the map yet; Bremer "covers an opening" only knows the built-in buildings; the old built-in Bunker / Recon / Shelter are still separate pieces.

### Next
- Make the old built-in structures use blueprints too (step 1–2 of section 9), then Side view from the blocks.
