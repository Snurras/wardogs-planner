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
- Bremer in front of an entrance or window (on the square right outside, face toward the building, face top above that opening's floor): the opening is **covered**. Attackers may walk on the footing if they can reach it (from the side along the row, or up from a step), but can't go through the face into the building, and can't crawl into a covered window. Open again only when that Bremer (or the column under it) is blown. Any other rotation leaves the opening usable from the footing. Code: `cov` on `portIn`/`portOut`, helper `covered()`.
- Buildings: entrances lead to the ground floor. Recon/Shelter bottom floor: only entrance squares and the open centre are floor, the rest is wall under the roof (`G.flr`/`G.cseal`); a sealed centre square blocks the way and can only be passed by blowing it. Recon floor 2 at H2 with windows; outside ladder opening = direct access (no C4). Windows (Bunker, Recon floor 2): 1 C4, crawl in from level with that floor.
- C4: blowing the top of a stack leaves what's below; blowing the bottom clears the column; each piece paid once per route. On-foot climb spots are assumed fixed first.

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
