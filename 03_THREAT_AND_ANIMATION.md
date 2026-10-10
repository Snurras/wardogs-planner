# 03 · Threat check & attack animation
Use for: how attackers get in, movement/C4 rules, the threat summary, the animated attack and its cast.

## Threat check (module `wd-threat`)
- Protected targets: emplacements, stations and the FOB. **Only FOB** tickbox (saved with the design) makes attackers go for the FOB alone.
- Summary: six rows (On foot, with C4, With a car, With a Ural Defender, …), each with a route to show and an attack to play (▶). “Show weak points on the map”. Details collapsible.

### Movement rules (facts)
- Step up 1 without jumping; drop any height. Jump a 1-block gap (straight, diagonal, two-across-one-over) landing up to 1 higher; long jump over a 2-block gap landing no higher. Jumps can't pass over anything higher than where you stand or squeeze between touching corners.
- Walk-through (doesn't block access): barbed wire, hedgehogs, recon tents, loudspeakers, builder's radios, emplacements, stations.
- Car roof reaches H3 (stand H2); Ural Defender roof reaches H4 (stand H3). Vehicles drive only on open ground.
- Bremer: footing H1 walkable and a step to an adjacent H2; face H3 can't be jumped from below; face across the wall line can be sneaked past on its footing; neighbouring faces on opposite sides leave a shooting gap (fire through, not walk); same side = tight seal; you can stand on a face top from H2 or a car (not through a higher face in between). Two faces back to back on one line: the higher wall counts, and both must be blown to open it.
- Bremer in front of an entrance or window (on the square right outside, face toward the building, face top above that opening's floor): the opening is **covered**. Attackers may walk on the footing if they can reach it (from the side along the row, or up from a step), but can't go through the face into the building, and can't crawl into a covered window. Open again only when that Bremer (or the column under it) is blown. Any other rotation leaves the opening usable from the footing. (A Bremer can't stand at the foot of a ladder: nothing can be built on that square, doc 02.) Helper `covered()`.
- Entrance opening height = Door height (`ht.door`, H2) above the building floor. Walk in/out only standing lower than the top of the opening: a block, raised footing or anything else right outside that reaches it closes the entrance (no dropping in from on top of it). Windows keep their own rule (stand level with that floor). (Side view draws the Bunker entrance 1.4h high: that is only the picture.)
- **Structures are groups of blocks** (since 10 Oct 2026, staging v123). `structParts(p)` (wd-custom) lists what stands: blueprint blocks (`pieceState`), Modify adds, entrance/centre seals (`p.closed`/`p.doors`) as blocks, roof slabs, windows, ladders. `threatGrid` puts each block in the cell column like any piece (`vBlock`, `.of` = the structure); `cellShape` turns a column into a surface height + **rooms** (space under a slab ≥ `ht.door` tall). Room moves: `passOK` (one step up, pass under the roof standing below it). C4 per block (corner = Large HESCO); blowing a block leaves the roof, so the square becomes a room. Windows hang from the roof (`G.hang`, not blown with the column), crawled through with `c4.window` into the room behind (`G.wins`); ladders lead to the room or open top at their height (`G.lads`). The old per-building code is gone.
- Buildings (rules the block model gives): Recon/Shelter bottom floor: only entrance squares and the open centre are floor, the rest is wall under the roof; a sealed centre square blocks the way and can only be passed by blowing it. Recon floor 2 at H2 with windows; outside ladder opening = direct access (no C4). Windows (Bunker, Recon floor 2): **1 C4 (`c4.window`, a guess: doc 11 says windows have no C4 and only go with a collapse — question 5)**, crawl in from level with that floor.
- Ladders: the square at a ladder's foot belongs to the ladder; nothing can be built there (`place()` refuses it both ways: a piece on the foot, or a structure whose foot lands on a piece). A ladder up to a floor under a roof (Recon floor 2) leads into that floor (`G.lads`). A ladder up to an **open top** (no roof over it: a Recon whose roof fell or was taken off, or a custom structure with a ladder and no floor 2, `TT(p).deck`) puts the attacker on the surface at that height, walked like any block.
- Modified structures (Modify structure, doc 02/11): heights, holes as extra entrances, windows, ladder and floor 2 come from what still stands (`TT(p)`, `structParts(p)`).
- C4: blowing the top of a stack leaves what's below; blowing the bottom clears the column; each piece paid once per route. On-foot climb spots are assumed fixed first.
- **Not yet in the threat check**: the 3×3 blast (one charge takes the blocks in the 3×3 squares around it, doc 11 §6.2) and collapse (blowing ground HESCO never brings a roof down here). So C4 counts for thick walls are too high. Corner HESCO is counted like a Large HESCO (4 C4), a guess: doc 11 question 6.

## Attack animation (module `wd-attack`)
- Camera doesn't follow: ▶ zooms to Fit and stays still.
- Vehicles drive in line with the weak point from N/E/S/W, park at 90° with a handbrake slide and skid marks (no duplicate car during the slide). Soldiers jump from the roof over the gate and never land on gates.
- Barbed wire: “Ouch” right after passing it (also gate wire); only the coils vibrate.
- Soldier look: green uniform, backpack, grey-black helmet, arm band, rifle or hammer (reused as the soldier in protection pictures).

### Cast and speech rules
- Friends in the cast: Snurra, Yaruto, Olle (+ others, see code).
- Yaruto/Snurra killing each other: “Betrayed by my own brother”. When HE is killed, add “De må være kommet over isen”.
- Olle killed: “Din idiot”; if Snurra killed him: “You are just like Darth Vader”.
- Anyone Olle kills: “Oh no, I thought you were my friend”; if it's Snurra: “Betrayed by my own son”.
