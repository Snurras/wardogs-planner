# 11 · Structures built from blocks (plan)
Use for: rebuilding Bunker, Recon Tower and Indirect Fire Shelter as real blocks instead of one piece with special rules; new or changed structures from game updates.
**Status: plan only, nothing built yet (8 Oct 2026).** Read with 01 (+ 03 for the threat check, + 04 for Side view).

**How to read this doc:** everything ending in **?** is an assumption made from how the planner works today. Snurra checks it in the game and either deletes the ? (true) or corrects it. Section 9 has the questions that can't be guessed.

---

## 1. Why
Today each structure is one big piece with rules attached: a height map, "raised" and "trimmed" areas, separate Trimmed pieces, lists of entrances / windows / ladders, and in the threat check separate floor maps (`bld`, `bld2`, `flr`, `cseal`). The code asks "is this a Recon Tower / Bunker?" in about twenty places. Every new game behaviour adds another check, and a game update that changes a structure means touching all of them.

## 2. The idea
- A structure is a **blueprint**: a list of blocks, floor by floor. Normal blocks (Small / Large HESCO) plus **hidden blocks** that can't be placed from the palette (wall, roof, window, ladder opening, entrance, top block).
- Placing a structure is still one click. The planner places all its blocks as **one group**.
- The threat check, Side view, heights and protection pictures read the blocks. They don't need to know which structure it is.
- A new or changed structure in the game = a new or edited blueprint (data), no new code.

## 3. The big change: squares get floors
Today the map stores **one top height per square**. Fine for HESCO (solid all the way up), wrong for buildings (roof at H2 with walkable space under it).
New: each square describes its **column**, e.g. "solid H0–1, open space H1–3, roof at H3". The attacker's route search moves between squares **and** between floors. This replaces the floor 1 / floor 2 workaround and covers any future building with more floors.

## 4. Hidden blocks (assumed catalogue)
| Block | What it is | Size | Walkable on top | C4 | Notes |
|---|---|---|---|---|---|
| **Wall square** | Solid part of a building under the roof (Recon / Shelter outer ring, floor 1) | 1×1, full floor height | — (roof above) | part of the outer wall, see 6 | not floor; you can't stand in it |
| **Room square** | Open floor inside a building, with a ceiling | 1×1 | — | 0 | the floor you walk on inside |
| **Roof slab** | Flat roof / floor between floors | 1×1, thin? | yes | ? | Recon: at H2 (floor 2) and at H4; Bunker at H2; Shelter at H2 |
| **Top block** | The raised centre on the roof | 1×1, H1 | yes | ? | Recon centre 2×2 (H4→H5), Shelter centre 3×3 (H2→H3). **Trimming = removing these.** |
| **Outer wall edge** | Thin wall on one side of a square (Bunker; Recon floor 2) | edge | no | Bunker 1? | like the Bremer face: a wall on a square's side, not a full square |
| **Entrance** | Opening in an outer wall, door height H2 above the floor | edge | — | 0 open; sealed = seal's C4 | sealable: Recon/Shelter Large HESCO or Door, Bunker Small HESCO only |
| **Window** | Small opening, crawl in level with that floor after blowing | edge | — | 1 | can be covered by a Bremer (doc 03) |
| **Ladder opening** | Outside ladder to Recon floor 2, open (no C4) | edge + the square below | — | 0 | can be covered by a Bremer at its foot (doc 03) |

Two kinds of wall are needed: **full squares** (Recon / Shelter ring) and **thin edges** (Bunker, Recon floor 2). The Bremer face already works as a thin edge, so the threat check knows that idea.

Evidence the top block is a real block: trimming takes 30 s on the Recon (4 squares) and 60 s on the Shelter (9 squares). Removing a piece takes 7 s, so 4 × 7 ≈ 30 and 9 × 7 ≈ 60. The trim is very likely "remove one block per square".

## 5. Blueprints (placed facing north, rotation 0; x = column 0→ east, y = row 0 → south)

### Bunker 4×4 · roof H2 · one floor
Floor 1 (H0–H2): **all 16 squares are room**? The walls are thin edges around the outside?
```
        x0  x1  x2  x3
  N   [ w   w   w   w ]     w = window in that square's outer edge
  y0  w .   .   .   . w
  y1  w .   .   .   . w
  y2  w .   .   .   . w
  y3  w .   .   .   . w
  S   [ w   w   E   w ]     E = entrance (x2), sealable with Small HESCO only
```
- Roof slab H2 on all 16 squares, walkable? No top block.
- Windows: every outer edge square except the entrance (15 windows)? Window floor = the bunker floor (its base).
- Can stand on HESCO up to H2: the whole blueprint moves up by its base height.
- C4 1 for the outer wall: blowing one **edge** opens one square?

### Recon Tower 4×4 · two floors · roof H4, centre H5
Floor 1 (H0–H2), ceiling = slab at H2:
```
        x0  x1  x2  x3
  y0    #   #   #   #
  y1    #   .   .   E       E (x3,y1) entrance, east side
  y2    E   .   .   #       E (x0,y2) entrance, west side
  y3    #   #   #   #       # = wall square, . = room (open centre 2×2)
```
- Entrance squares are room too (the opening is on their outer edge)?
- Centre 2×2 can be closed with Large HESCO or Door (today keys 100+). In the block model these become real blocks, so **the threat check finally sees them**?
- Floor 1 and floor 2 are **not connected inside** (no stairs)?

Floor 2 (H2–H4), floor = slab at H2, ceiling = roof slab at H4:
```
        x0  x1  x2  x3
  N   [ -   w   w   - ]
  y0    .   .   .   .
  y1  w .   .   .   . w
  y2  w .   .   .   . w
  y3    .   L   .   .
  S   [ -   L   -   - ]     L = ladder opening (x1, south edge), - = plain outer wall edge
```
- All 16 squares are room on floor 2? Thin outer wall edges all round?
- Windows: N x1–x2, W y1–y2, E y1–y2 (6 windows)? None on the south side?
- Ladder: outside the south edge at x1, leads straight into floor 2, no C4?
- Roof: slab at H4 on all 16, walkable? Top block on the centre 2×2 (H4→H5)?
- Trimmed Recon = Recon with the 4 top blocks removed (no separate piece any more)?

### Indirect Fire Shelter 5×5 · one floor · roof H2, centre H3
Floor 1 (H0–H2), ceiling = roof slab at H2:
```
        x0  x1  x2  x3  x4
  y0    #   #   E   #   #
  y1    #   .   .   .   #
  y2    E   .   .   .   E
  y3    #   .   .   .   #
  y4    #   #   E   #   #       4 entrances, middle of each side; centre 3×3 open
```
- Roof slab H2 on all 25, walkable? Top block on the centre 3×3 (H2→H3)?
- No windows, no second floor?
- Trimmed Shelter = Shelter with the 9 top blocks removed?
- Centre 3×3 can be closed with Large HESCO or Door?

### Not structures in this sense (stay as normal pieces)
Loudspeaker, Builder's Radio, Bremer, Door, Gate, stations, emplacements. They have no inside to walk in?

## 6. C4 and collapse (assumed)
Today: Bunker 1 C4 "for the outer wall", Recon and Shelter 4 C4; only the outer wall has to go.
- C4 blows **one block**, the same as on a HESCO stack?
- Bunker: 1 C4 on an outer wall edge opens that one square into the room?
- Recon / Shelter: 4 C4 on a wall square removes that square; you can then walk into the room behind it?
- Blowing a roof slab or top block: possible? How much C4?
- Window: 1 C4 opens a crawl hole (doc 03, unchanged).
- **Collapse:** each blueprint has a list of "if all these blocks are gone, the whole structure falls". Assumed starting point:
  - Bunker never collapses from one blown edge?
  - Recon: if the 4 corner wall squares are all gone, the tower falls?
  - Shelter: if the 4 corner wall squares are all gone, the shelter falls?
  - Things standing on a fallen structure fall too (they lose their support)?
- A collapsed structure leaves no rubble that blocks movement?

## 7. Planner behaviour (decided unless Snurra says otherwise)
- One structure = one thing in the planner: Select, Move, Rotate, Erase, Brush, copy/paste and the build order treat the group as a unit.
- Haul and build time count the structure ("1 Recon Tower: 61 supplies, 8 s"), never its hidden blocks. Trimming keeps its own extra time (30 s / 60 s).
- Hidden blocks are not in the palette. They show in Side view, the hover picture, and when choosing a part to remove.
- **Saving:** store the structure plus its changes ("Recon Tower at X, minus top blocks", "entrance 2 sealed with a Door"), not every block. Saves stay small, and fixing a blueprint updates old designs. Old saves (`recon_trim`, `ifs_trim`, `closed`, `doors`) load as the matching structure + changes.
- Fact sheet keeps the numbers (heights, C4). Blueprint shapes live in the code next to the piece catalogue `P`.

## 8. Plan of work (each step can go on test by itself)
1. **Blueprints + blocks inside the threat check only.** No visible change. Run all templates and some saved designs through the old and the new check; fix the new one until both give the same routes and C4.
2. **Heights, Side view, protection pictures** read the blocks. Remove the old height maps, `raised`/`trimmed`, `bld`/`bld2`/`flr`/`cseal` and the `recon_trim` / `ifs_trim` pieces.
3. **New features:** remove parts of a structure, trim from the map, collapse rules in the threat check and the attack animation (blown blocks shown as holes).

Code today (v105, see 01 code map): piece catalogue `P` (`bunker`, `ifs`, `recon_tower`, `recon_trim`, `ifs_trim`, ~line 979); heights from the Fact sheet ~line 1085; entrances / centre / windows / ladder helpers ~line 1094–1130; threat grid `threatGrid()` ~line 2850; Side view drawing of buildings ~line 1866.

## 9. Questions for the game (can't be guessed)
Answer like the questionnaire: a short text list + 1–2 photos. Correct any **?** above at the same time.
1. **Wall C4:** Recon / Shelter "4 C4": does it blow **one wall square**, or a whole side, or the whole building?
2. **Bunker C4:** 1 C4 on the outer wall: what is left? A one-square hole? Can you walk in through it standing on the ground?
3. **Collapse:** what makes a whole structure fall? Number of wall squares, corners, a specific part? Does a fallen structure leave anything behind?
4. **Roof:** can a roof slab or top block be blown? How much C4? Do you fall into the room below?
5. **Floor 2:** if the Recon slab at H2 is blown, are floor 1 and floor 2 joined?
6. **Inside height:** Recon floor 2 — can you stand up straight (room H2–H4)? Bunker room H0–H2?
7. **Partial removal with the hammer:** besides trimming, can any other part be removed (one wall square, one roof square, the ladder)? Same 7 s each?
8. **Rebuild:** after a part is blown, can it be repaired, or must the whole structure be rebuilt? Cost?
9. **Bunker windows:** really one in every outer square except the entrance (15)? Corner squares have windows on both sides?
10. **Recon windows:** exactly N x1–x2, W y1–y2, E y1–y2? None facing south (ladder side)?
11. **Shelter:** any windows or firing slits? Can you stand on the roof ring at H2?
12. **Anything on top:** can HESCO or other pieces be built on a roof today (Bunker / Recon / Shelter)? Doc 02 says "anything on a building up to H10" — on which squares?
13. **Health instead of C4:** do structure parts have hit points (rockets, mortar, vehicle guns), or only C4?
14. **Game updates:** any announced new structures or changes? (Name + size + photo is enough to start a blueprint.)
